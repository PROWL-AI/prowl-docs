---
name: majestic_download_back_links
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_download_back_links`

START AN ASYNC EXPORT JOB for the full backlink set of a domain/URL (beyond the 50k row cap of majestic_get_back_link_data).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_download_back_links",
  "params": {
    "item": "majestic.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item` | string | yes |  | Root domain, subdomain, or URL to export |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `skip_if_analysis_cost_greater_than` | integer | no | `100000` | Abort if the job would cost more analysis units than this |
| `use_prefix_scan` | boolean | no | `False` |  |
| `unique_backlinks_only` | boolean | no | `False` | One backlink per source→target pair |
| `counts_only` | boolean | no | `False` | Counts-per-URL summary instead of link rows |
| `min_backlinks` | integer | no | `0` | With counts_only: minimum backlinks per URL |
| `exclude_deleted` | boolean | no | `False` |  |
| `exclude_nofollow` | boolean | no | `False` |  |
| `min_trust_flow` | integer | no | `0` |  |
| `max_trust_flow` | integer | no | `100` |  |
| `min_citation_flow` | integer | no | `0` |  |
| `max_citation_flow` | integer | no | `100` |  |
| `date_from` | string | no |  | YYYY-MM-DD last-crawled window start (needs date_to) |
| `date_to` | string | no |  | YYYY-MM-DD last-crawled window end |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item": {
      "type": "string",
      "description": "Root domain, subdomain, or URL to export"
    },
    "datasource": {
      "type": "string",
      "enum": [
        "fresh",
        "historic"
      ],
      "default": "fresh",
      "description": "Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data)"
    },
    "skip_if_analysis_cost_greater_than": {
      "type": "integer",
      "default": 100000,
      "minimum": 1,
      "description": "Abort if the job would cost more analysis units than this"
    },
    "use_prefix_scan": {
      "type": "boolean",
      "default": false
    },
    "unique_backlinks_only": {
      "type": "boolean",
      "default": false,
      "description": "One backlink per source\u2192target pair"
    },
    "counts_only": {
      "type": "boolean",
      "default": false,
      "description": "Counts-per-URL summary instead of link rows"
    },
    "min_backlinks": {
      "type": "integer",
      "default": 0,
      "description": "With counts_only: minimum backlinks per URL"
    },
    "exclude_deleted": {
      "type": "boolean",
      "default": false
    },
    "exclude_nofollow": {
      "type": "boolean",
      "default": false
    },
    "min_trust_flow": {
      "type": "integer",
      "default": 0,
      "minimum": 0,
      "maximum": 100
    },
    "max_trust_flow": {
      "type": "integer",
      "default": 100,
      "minimum": 0,
      "maximum": 100
    },
    "min_citation_flow": {
      "type": "integer",
      "default": 0,
      "minimum": 0,
      "maximum": 100
    },
    "max_citation_flow": {
      "type": "integer",
      "default": 100,
      "minimum": 0,
      "maximum": 100
    },
    "date_from": {
      "type": "string",
      "description": "YYYY-MM-DD last-crawled window start (needs date_to)"
    },
    "date_to": {
      "type": "string",
      "description": "YYYY-MM-DD last-crawled window end"
    }
  },
  "required": [
    "item"
  ]
}
```

## Example request

```json
{
  "item": "majestic.com"
}
```

## Output

Job handle, not data

Key fields: `job_id`, `status`, `next`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| invalid_api_key | Majestic rejected the API key (Code != OK, e.g. InvalidAPIKey). | Verify MAJESTIC_API_KEY and that API access is enabled on the Majestic account (API tab). |
| insufficient_units | Analysis / retrieval / index-item resource units exhausted for the billing period. | Check remaining units via majestic_get_subscription_info; reduce count/items or wait for period reset. |
| rate_limit | Too many requests (SearchByKeyword is limited to 3 requests/second per account). | Retry with backoff; the provider pool already throttles concurrency. |
| invalid_item | Item/domain/URL malformed or not present in the chosen index. | Pass a bare root domain (example.com), subdomain, or full URL; try datasource=historic for older items. |
| prefix_scan_not_possible | use_prefix_scan=True failed with RealTimePrefixQueryNotPossible for a large item. | Pre-check with majestic_get_prefix_query_estimate; fall back to majestic_download_back_links. |

## When to use

- ALWAYS pre-check cost: majestic_get_index_item_info → DownloadBacklinksAnalysisResUnitsCost
- Files expire ~7 days after completion; delete with majestic_delete_downloads when done

- Chain dependency: read `DownloadBacklinksAnalysisResUnitsCost` from `majestic_get_index_item_info` and pass it as `skip_if_analysis_cost_greater_than` so the job is only created when the cost is acceptable.

**Chain inputs:** `{'param': 'skip_if_analysis_cost_greater_than', 'from_tool': 'majestic_get_index_item_info', 'extract': 'DataTables.Results.Data[].DownloadBacklinksAnalysisResUnitsCost'}`

**Chain groups:** `majestic`, `majestic_download_jobs`

## Alternatives

- `moz_v2_index_metadata`
- `spyfu_find_also_buys_ads_keywords`
- `spyfu_get_ad_history`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
