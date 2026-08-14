---
name: majestic_get_anchor_text
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_anchor_text`

Anchor-text distribution for an item: aggregated phrases (mode=0), per-referring-domain (mode=1), or raw backlinks (mode=2, only when the index reports CanReturnURLs=1).

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
  "tool_name": "majestic_get_anchor_text",
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
| `text_mode` | enum(0, 1) | no | `0` | 0=raw lowercase; 1=cleaned |
| `mode` | enum(0, 1, 2) | no | `0` | 0=aggregated anchors; 1=referring domains; 2=backlink rows |
| `filter_anchor_text` | string | no |  |  |
| `filter_anchor_text_mode` | enum(0, 1, 2) | no | `0` | 0=off; 1=exact; 2=contains |
| `filter_ref_domain` | string | no |  | With mode=2: restrict to one referring domain |
| `count` | integer | no | `10` |  |
| `from_offset` | integer | no | `0` |  |
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
    "text_mode": {
      "type": "integer",
      "enum": [
        0,
        1
      ],
      "default": 0,
      "description": "0=raw lowercase; 1=cleaned"
    },
    "mode": {
      "type": "integer",
      "enum": [
        0,
        1,
        2
      ],
      "default": 0,
      "description": "0=aggregated anchors; 1=referring domains; 2=backlink rows"
    },
    "filter_anchor_text": {
      "type": "string"
    },
    "filter_anchor_text_mode": {
      "type": "integer",
      "enum": [
        0,
        1,
        2
      ],
      "default": 0,
      "description": "0=off; 1=exact; 2=contains"
    },
    "filter_ref_domain": {
      "type": "string",
      "description": "With mode=2: restrict to one referring domain"
    },
    "count": {
      "type": "integer",
      "default": 10,
      "minimum": 1,
      "maximum": 1000
    },
    "from_offset": {
      "type": "integer",
      "default": 0,
      "minimum": 0
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

Mode 0 → DataTables.AnchorText; mode 1 → RefDomains; mode 2 → BackLinks

Key fields: `DataTables.AnchorText.Data[].AnchorText`, `DataTables.AnchorText.Data[].RefDomains`, `DataTables.AnchorText.Data[].TotalLinks`

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

- Check the CanReturnURLs header from a mode 0/1 call before requesting mode=2

## Alternatives

- `dataforseo_bl_anchors`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
