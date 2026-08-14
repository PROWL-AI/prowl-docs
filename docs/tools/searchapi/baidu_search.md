---
name: baidu_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `baidu_search`

Baidu Web Search — Chinese search engine.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "baidu_search",
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
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
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

Top-level keys: `search_metadata`, `search_parameters`, `knowledge_graph`, `organic_results`, `top_searches`, `related_searches`, `people_also_search_for`, `pagination`

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
| `knowledge_graph` | object |  |
| `knowledge_graph.title` | string |  |
| `knowledge_graph.link` | string |  |
| `knowledge_graph.sitelinks` | object |  |
| `knowledge_graph.sitelinks.inline[]` | array<object> |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].displayed_link` | string |  |
| `organic_results[].snippet` | string |  |
| `organic_results[].snippet_highlighted_words[]` | array<string> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_1g3L6weL3bSxlr09MkpaP2rB",
    "status": "Success",
    "created_at": "2026-03-28T20:44:18Z",
    "request_time_taken": 2.08,
    "parsing_time_taken": 0.01,
    "total_time_taken": 2.1,
    "request_url": "https://www.baidu.com/s?wd=instagram.com&base_query=instagram.com&oq=instagram.com&f=8&tn=baidu&ie=utf-8",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_1g3L6weL3bSxlr09MkpaP2rB.html",
    "json_url": "https://www.searchapi.io/api/
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

- SearchAPI.io engine tool — set locale/geo params when available for market-correct results
- Use a prior search/list tool to obtain IDs before detail/reviews calls

## Alternatives

- `serpapi_baidu`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
