---
name: majestic_download_ref_domain_back_links
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_download_ref_domain_back_links`

START AN ASYNC EXPORT JOB for the full referring-domain set (beyond majestic_get_ref_domains' 100k analysis cap) with top backlinks per referring domain.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `domain`, `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_download_ref_domain_back_links",
  "params": {
    "item": "majestic.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item` | string | yes |  | Root domain, subdomain, or URL |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `max_source_urls_per_ref_domain` | integer | no | `10` |  |
| `mode` | enum(0, 1) | no | `0` | 0=all links incl deleted; 1=exclude deleted |
| `skip_if_analysis_cost_greater_than` | integer | no | `100000` |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item": {
      "type": "string",
      "description": "Root domain, subdomain, or URL"
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
    "max_source_urls_per_ref_domain": {
      "type": "integer",
      "default": 10,
      "minimum": 1,
      "maximum": 10
    },
    "mode": {
      "type": "integer",
      "enum": [
        0,
        1
      ],
      "default": 0,
      "description": "0=all links incl deleted; 1=exclude deleted"
    },
    "skip_if_analysis_cost_greater_than": {
      "type": "integer",
      "default": 100000,
      "minimum": 1
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

Job handle

Key fields: `job_id`, `eta`, `status`, `next`

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

- A 100k-ref-domain site costs ~2.05M analysis units — raise the skip guard deliberately, never blindly

- Chain dependency: pre-check cost with `majestic_get_index_item_info` (RefDomains) before creating the job.

**Chain groups:** `majestic_download_jobs`

## Alternatives

- `moz_linking_domains`
- `moz_v2_global_top_root_domains`
- `moz_v2_index_metadata`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
