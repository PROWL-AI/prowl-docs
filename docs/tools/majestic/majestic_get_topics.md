---
name: majestic_get_topics
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_topics`

Topical Trust Flow breakdown for an item: which topics the linking web assigns to it, with links/pages/ref-domain counts per topic.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_topics",
  "params": {
    "item": "majestic.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item` | string | yes |  | Domain, subdomain, or URL |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `count` | integer | no | `100` |  |
| `from_offset` | integer | no | `1` | 1-based pagination start |
| `sort_by` | enum(trust&flowlinks, topic, links, pages, refdomains, linksfromrefdomains) | no | `trust&flowlinks` |  |
| `sort_order` | enum(asc, desc) | no | `desc` |  |
| `use_prefix_scan` | boolean | no | `False` |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item": {
      "type": "string",
      "description": "Domain, subdomain, or URL"
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
      "minimum": 1
    },
    "from_offset": {
      "type": "integer",
      "default": 1,
      "minimum": 1,
      "description": "1-based pagination start"
    },
    "sort_by": {
      "type": "string",
      "default": "trust&flowlinks",
      "enum": [
        "trust&flowlinks",
        "topic",
        "links",
        "pages",
        "refdomains",
        "linksfromrefdomains"
      ]
    },
    "sort_order": {
      "type": "string",
      "enum": [
        "asc",
        "desc"
      ],
      "default": "desc"
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

DataTables.Topics rows

Key fields: `DataTables.Topics.Data[].Topic`, `DataTables.Topics.Data[].TopicalTrustFlow`, `DataTables.Topics.Data[].RefDomains`

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

- Topical mismatch between a domain and its link profile is a spam/toxicity signal

## Alternatives

_None listed._

## Provider docs

https://developer-support.majestic.com/api/commands/
