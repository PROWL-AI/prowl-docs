---
name: google_trends
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_trends`

Google Trends — interest over time for a keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `searchapi`, `trends` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_trends",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Search query |
| `geo` | string | no |  | Geo code (e.g. 'US', 'GB') |
| `data_type` | enum(TIMESERIES, GEO_MAP, RELATED_TOPICS, RELATED_QUERIES) | no |  | Type of trend data |
| `time` | string | no |  | Time range (e.g. 'today 12-m', 'today 3-m') |
| `cat` | integer | no |  | Category ID |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "geo": {
      "type": "string",
      "description": "Geo code (e.g. 'US', 'GB')"
    },
    "data_type": {
      "type": "string",
      "description": "Type of trend data",
      "enum": [
        "TIMESERIES",
        "GEO_MAP",
        "RELATED_TOPICS",
        "RELATED_QUERIES"
      ]
    },
    "time": {
      "type": "string",
      "description": "Time range (e.g. 'today 12-m', 'today 3-m')"
    },
    "cat": {
      "type": "integer",
      "description": "Category ID"
    }
  },
  "required": [
    "q"
  ]
}
```

## Example request

```json
{
  "q": "example query"
}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Unsupported value `` in data_type parameter."
}
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SEARCH_API_KEY | Skip SearchAPI tools — use Exa or Perplexity as alternatives for web search |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 422 | Invalid parameters | Check query and filter parameters match the expected format |

## When to use

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

## Alternatives

- `google_news`
- `dataforseo_kw_google_trends_explore`
- `dataforseo_kw_dataforseo_trends_explore`
- `serpapi_google_trends`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
