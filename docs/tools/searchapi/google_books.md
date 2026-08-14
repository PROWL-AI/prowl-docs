---
name: google_books
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_books`

Google Books — search books by title, author, or topic.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_books",
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
| `gl` | string | no |  | Country of the search, ISO alpha-2 (SearchAPI defaults to 'us'). Defaults to the run's market when one was stated. |
| `hl` | string | no | `en` | Language code (default 'en') |
| `num` | integer | no |  | Number of results to return |
| `tbm` | string | no |  | Book type filter |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "gl": {
      "type": "string",
      "description": "Country of the search, ISO alpha-2 (SearchAPI defaults to 'us'). Defaults to the run's market when one was stated."
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
    "tbm": {
      "type": "string",
      "description": "Book type filter"
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

Top-level keys: `search_metadata`, `search_parameters`, `organic_results`, `pagination`

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
| `search_parameters.gl` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].id` | string |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].authors[]` | array<object> |  |
| `organic_results[].date` | string |  |
| `organic_results[].extensions[]` | array<string> |  |
| `organic_results[].found_in` | string |  |
| `organic_results[].snippet` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_1XbZBxkZENuMAbZD6v8JaLNR",
    "status": "Success",
    "created_at": "2026-03-28T20:43:57Z",
    "request_time_taken": 3.17,
    "parsing_time_taken": 0.02,
    "total_time_taken": 3.19,
    "request_url": "https://www.google.com/search?q=instagram.com&gl=us&hl=en&tbs=&tbm=bks",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_1XbZBxkZENuMAbZD6v8JaLNR.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_1XbZBxkZENuMAb
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

- `google_about_this_domain`
- `google_ads_transparency_advertiser_search`
- `google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
