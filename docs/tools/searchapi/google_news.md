---
name: google_news
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_news`

Google News — search news articles.

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
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_news",
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
| `location` | string | no |  | Location for geo-targeted results (e.g. 'New York, NY') |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'New York, NY')"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `pagination`

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
| `search_parameters.device` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.time_taken_displayed` | number |  |
| `search_information.detected_location` | string |  |
| `search_information.has_no_results_for` | boolean |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_mOgBEZe50gHNw58NMkzwL3jW",
    "status": "Success",
    "created_at": "2026-03-28T20:43:51Z",
    "request_time_taken": 1.15,
    "parsing_time_taken": 0.01,
    "total_time_taken": 1.15,
    "request_url": "https://www.google.com/search?q=instagram.com&oq=instagram.com&gl=us&hl=en&tbm=nws&tbs=&ie=UTF-8",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_mOgBEZe50gHNw58NMkzwL3jW.html",
    "json_url": "https://www.searchapi.io/api/v1/sear
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

**Chain groups:** `searchapi_news`

## Alternatives

- `google_trends`
- `serpapi_google_news`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
