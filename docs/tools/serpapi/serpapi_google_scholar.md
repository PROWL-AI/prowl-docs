---
name: serpapi_google_scholar
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_scholar`

Google Scholar academic search via SerpAPI — research papers and citations.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_scholar",
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
| `as_ylo` | integer | no |  | Start year filter |
| `as_yhi` | integer | no |  | End year filter |
| `hl` | string | no | `en` | Language code (default 'en') |
| `num` | integer | no |  | Number of results to return |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "as_ylo": {
      "type": "integer",
      "description": "Start year filter"
    },
    "as_yhi": {
      "type": "integer",
      "description": "End year filter"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `related_searches`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_scholar_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.hl` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.time_taken_displayed` | number |  |
| `search_information.query_displayed` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].result_id` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].snippet` | string |  |
| `organic_results[].publication_info` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d80e3e1766c96bc4d33",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/ayJmKhOp9AVAqbXaikWlNA/69c83d80e3e1766c96bc4d33.json",
    "created_at": "2026-03-28 20:43:44 UTC",
    "processed_at": "2026-03-28 20:43:44 UTC",
    "google_scholar_url": "https://scholar.google.com/scholar?q=instagram.com&hl=en",
    "raw_html_file": "https://serpapi.com/searches/ayJmKhOp9AVAqbXaikWlNA/69c83d80e3e1766c96bc4d33.html",
    "total_time_taken"
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

- `google_scholar`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
