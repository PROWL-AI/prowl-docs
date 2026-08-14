---
name: majestic_search_by_keyword
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_search_by_keyword`

Search the Majestic index for URLs (scope=2) or root domains (scope=0) matching a keyword, ranked by relevance with TrustFlow/CitationFlow per result.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `keywords`, `majestic`, `search`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_search_by_keyword",
  "params": {
    "query": "project management"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Keyword or phrase |
| `scope` | enum(0, 2) | no | `2` | 0=root domains; 2=URLs |
| `count` | integer | no | `10` |  |
| `from_offset` | integer | no | `0` |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Keyword or phrase"
    },
    "scope": {
      "type": "integer",
      "enum": [
        0,
        2
      ],
      "default": 2,
      "description": "0=root domains; 2=URLs"
    },
    "count": {
      "type": "integer",
      "default": 10,
      "minimum": 1,
      "maximum": 100
    },
    "from_offset": {
      "type": "integer",
      "default": 0,
      "minimum": 0,
      "maximum": 1000
    }
  },
  "required": [
    "query"
  ]
}
```

## Example request

```json
{
  "query": "project management"
}
```

## Output

DataTables.Results rows ranked by SearchScore

Key fields: `DataTables.Results.Data[].Item`, `DataTables.Results.Data[].SearchScore`, `DataTables.Results.Data[].TrustFlow`

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

- scope=0 finds authority domains for a topic — useful for niche-media and digital-PR prospecting

## Alternatives

- `exa_keyword_search`
- `dataforseo_keywords_bing_search_volume_history`
- `moz_keyword_difficulty`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
