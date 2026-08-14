---
name: majestic_get_top_pages
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_top_pages`

Top URLs of a domain/subdomain by backlink metrics (ACRank, TrustFlow, ExtBackLinks) plus a domain summary table — the only guaranteed 'is this URL in the index' check.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `majestic`, `onpage`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_top_pages",
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
| `count` | integer | no | `10` |  |
| `start_doc` | integer | no | `0` | Paging offset |
| `use_prefix_scan` | boolean | no | `False` | Treat item as path prefix |

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
    "count": {
      "type": "integer",
      "default": 10,
      "minimum": 1,
      "maximum": 10000
    },
    "start_doc": {
      "type": "integer",
      "default": 0,
      "minimum": 0,
      "description": "Paging offset"
    },
    "use_prefix_scan": {
      "type": "boolean",
      "default": false,
      "description": "Treat item as path prefix"
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

DataTables.Matches (pages) + DataTables.DomainInfo (summary)

Key fields: `DataTables.Matches.Data[].URL`, `DataTables.Matches.Data[].TrustFlow`, `DataTables.Matches.Data[].ExtBackLinks`, `DataTables.DomainInfo.Data[].RefDomains`

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

- FlagPageData=True → Date is last crawl; False → Date is first backlink sighting

## Alternatives

- `moz_top_pages`
- `moz_v2_global_top_pages`
- `moz_v2_top_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
