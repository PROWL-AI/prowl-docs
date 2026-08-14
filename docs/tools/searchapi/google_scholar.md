---
name: google_scholar
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_scholar`

Google Scholar — search academic papers, citations, and scholarly articles.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_scholar",
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
| `hl` | string | no | `en` | Language code (default 'en') |
| `num` | integer | no |  | Number of results to return |
| `as_ylo` | integer | no |  | Published from year (e.g. 2020) |
| `as_yhi` | integer | no |  | Published until year (e.g. 2025) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "num": {
      "type": "integer",
      "description": "Number of results to return",
      "minimum": 1,
      "maximum": 100
    },
    "as_ylo": {
      "type": "integer",
      "description": "Published from year (e.g. 2020)"
    },
    "as_yhi": {
      "type": "integer",
      "description": "Published until year (e.g. 2025)"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `related_searches`, `pagination`

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
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.page` | integer |  |
| `search_information.time_taken_displayed` | number |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].data_cid` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].publication` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_1g3L6weL3bSxlr0bBkpaP2rB",
    "status": "Success",
    "created_at": "2026-03-28T20:43:55Z",
    "request_time_taken": 0.36,
    "parsing_time_taken": 0.01,
    "total_time_taken": 0.37,
    "request_url": "https://scholar.google.com/scholar?q=instagram.com&hl=en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_1g3L6weL3bSxlr0bBkpaP2rB.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_1g3L6weL3bSxlr0bBkpaP2rB"
  
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

- `serpapi_google_scholar`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
