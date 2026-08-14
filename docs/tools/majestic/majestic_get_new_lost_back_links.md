---
name: majestic_get_new_lost_back_links
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_new_lost_back_links`

New (mode=0) or lost (mode=1) backlinks for an item within a date range.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_new_lost_back_links",
  "params": {
    "item": "majestic.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item` | string | yes |  | Domain, subdomain, or full URL |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `count` | integer | no | `100` |  |
| `mode` | enum(0, 1) | no | `0` | 0=new links; 1=lost links |
| `date_from` | string | no |  | YYYY-MM-DD (default: most recent backlink date) |
| `date_to` | string | no |  | YYYY-MM-DD (default: date_from + 1 day) |
| `use_prefix_scan` | boolean | no | `False` |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item": {
      "type": "string",
      "description": "Domain, subdomain, or full URL"
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
      "default": 100,
      "minimum": 1,
      "maximum": 1000
    },
    "mode": {
      "type": "integer",
      "enum": [
        0,
        1
      ],
      "default": 0,
      "description": "0=new links; 1=lost links"
    },
    "date_from": {
      "type": "string",
      "description": "YYYY-MM-DD (default: most recent backlink date)"
    },
    "date_to": {
      "type": "string",
      "description": "YYYY-MM-DD (default: date_from + 1 day)"
    },
    "use_prefix_scan": {
      "type": "boolean",
      "default": false
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

DataTables.BackLinks rows (same shape as majestic_get_back_link_data)

Key fields: `DataTables.BackLinks.Data[].SourceURL`, `DataTables.BackLinks.Data[].Date`, `DataTables.BackLinks.Data[].ReasonLost`

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

- Call majestic_get_new_lost_back_link_calendar first — out-of-range dates return errors
- A 30-day range costs 15,000 analysis units; prefer ≤7-day windows

**Chain inputs:** `{'param': 'date_from', 'from_tool': 'majestic_get_new_lost_back_link_calendar', 'extract': 'DataTables.Calendar.Data[].Date'}`

**Chain groups:** `majestic`

## Alternatives

_None listed._

## Provider docs

https://developer-support.majestic.com/api/commands/
