---
name: serpapi_naver
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_naver`

Naver Web Search via SerpAPI — Korean search engine.

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
  "tool_name": "serpapi_naver",
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
| `where` | enum(web, blog, news, shop, image, video) | no |  | Search type |
| `start` | integer | no |  | Result offset |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "where": {
      "type": "string",
      "description": "Search type",
      "enum": [
        "web",
        "blog",
        "news",
        "shop",
        "image",
        "video"
      ]
    },
    "start": {
      "type": "integer",
      "description": "Result offset"
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

Top-level keys: `search_metadata`, `search_parameters`, `related_results`, `news_results`, `web_results`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.naver_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.query` | string |  |
| `search_parameters.engine` | string |  |
| `search_parameters.device` | string |  |
| `related_results[]` | array<object> |  |
| `related_results[].position` | integer |  |
| `related_results[].title` | string |  |
| `related_results[].link` | string |  |
| `news_results[]` | array<object> |  |
| `news_results[].position` | integer |  |
| `news_results[].title` | string |  |
| `news_results[].link` | string |  |
| `news_results[].thumbnail` | string |  |
| `news_results[].news_info` | object |  |
| `news_results[].snippet` | string |  |
| `news_results[].related_news[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8b14537b2030883355",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/0vSWqQK0DEwn7ERISYkubw/69c83d8b14537b2030883355.json",
    "created_at": "2026-03-28 20:43:55 UTC",
    "processed_at": "2026-03-28 20:43:55 UTC",
    "naver_url": "https://search.naver.com/search.naver?query=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/0vSWqQK0DEwn7ERISYkubw/69c83d8b14537b2030883355.html",
    "total_time_taken": 1.95
 
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

- `naver_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
