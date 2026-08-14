---
name: serpapi_bing_news
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_bing_news`

Bing News search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_bing_news",
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
| `mkt` | string | no |  | Market code |
| `freshness` | enum(Day, Week, Month) | no |  | Freshness filter |
| `count` | integer | no |  | Number of results |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "mkt": {
      "type": "string",
      "description": "Market code"
    },
    "freshness": {
      "type": "string",
      "description": "Freshness filter",
      "enum": [
        "Day",
        "Week",
        "Month"
      ]
    },
    "count": {
      "type": "integer",
      "description": "Number of results",
      "minimum": 1,
      "maximum": 50
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `error`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.bing_news_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d87d17a809dc4f40c0b",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/7hpcTWneu6lbty3DZc5nDg/69c83d87d17a809dc4f40c0b.json",
    "created_at": "2026-03-28 20:43:51 UTC",
    "processed_at": "2026-03-28 20:43:51 UTC",
    "bing_news_url": "https://www.bing.com/news/search?q=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/7hpcTWneu6lbty3DZc5nDg/69c83d87d17a809dc4f40c0b.html",
    "total_time_taken": 0.73
  },
 
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SERP_API_KEY | Check SERP_API_KEY in .env or SerpAPI dashboard |
| 429 | Monthly rate limit reached | Upgrade SerpAPI plan or wait for quota reset |
| 400 | Missing required parameters | Check query and engine parameters |

## When to use

- SerpAPI engine is encoded in the tool name — do not re-pass engine unless the schema requires it
- Prefer the SearchAPI twin when cost/coverage is better for the same surface
- Paginate with num/start (or page) when result sets are truncated

## Alternatives

- `bing_news`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
