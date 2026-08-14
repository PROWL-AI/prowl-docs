---
name: majestic_get_keyword_info
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_keyword_info`

Phrase-match and broad-match occurrence counts for up to 1000 keywords across the Majestic index (in titles, URLs, anchor texts) — a link-graph-based keyword demand signal.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `keywords`, `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_keyword_info",
  "params": {
    "keywords": [
      "backlink checker",
      "seo audit"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | string[] | yes |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "maxItems": 1000
    }
  },
  "required": [
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": [
    "backlink checker",
    "seo audit"
  ]
}
```

## Output

DataTables.Keywords rows (one per keyword)

Key fields: `DataTables.Keywords.Data[].Keyword`, `DataTables.Keywords.Data[].PhraseSearchVolume`, `DataTables.Keywords.Data[].BroadSearchVolume`

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

- Counts measure index presence, not Google search volume — combine with dataforseo keyword tools

## Alternatives

- `moz_keyword_difficulty`
- `moz_keyword_metrics`
- `moz_keyword_opportunity`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
