---
name: google_finance
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_finance`

Google Finance — stock prices, market data, and financial information.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `finance`, `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_finance",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Stock ticker or company name (e.g. 'GOOG', 'Apple') |
| `hl` | string | no | `en` | Language code (default 'en') |
| `window` | enum(1D, 5D, 1M, 6M, 1Y, 5Y) | no |  | Time window |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Stock ticker or company name (e.g. 'GOOG', 'Apple')"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "window": {
      "type": "string",
      "description": "Time window",
      "enum": [
        "1D",
        "5D",
        "1M",
        "6M",
        "1Y",
        "5Y"
      ]
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

Top-level keys: `search_metadata`, `search_parameters`, `error`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.request_time_taken` | number |  |
| `search_metadata.parsing_time_taken` | number |  |
| `search_metadata.total_time_taken` | number |  |
| `search_metadata.request_url` | string |  |
| `search_metadata.html_url` | string |  |
| `search_metadata.json_url` | string |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.hl` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_gM5dQzeGq7sxK5WROvOlAjp3",
    "status": "Success",
    "created_at": "2026-03-28T20:43:57Z",
    "request_time_taken": 0.74,
    "parsing_time_taken": 0.01,
    "total_time_taken": 0.75,
    "request_url": "https://www.google.com/finance/quote/instagram.com?hl=en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_gM5dQzeGq7sxK5WROvOlAjp3.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_gM5dQzeGq7sxK5WROvOlAjp3"
  
...
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

- `dataforseo_serp_google_finance_quote`
- `dataforseo_serp_google_finance_explore`
- `serpapi_google_finance`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
