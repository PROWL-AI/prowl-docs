---
name: google_patents
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_patents`

Google Patents — search patents by keywords, inventors, or assignees.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `google`, `patents`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_patents",
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
| `countries` | string | no |  | Jurisdiction filter — ISO 3166-1 alpha-2 codes, comma separated (e.g. 'US,DE'). Defaults to the run's market when one was stated. |
| `language` | string | no |  | Patent language NAME, not a code — e.g. 'ENGLISH', 'SWEDISH'. Comma-separate for several. |
| `num` | integer | no |  | Number of results to return |
| `scholar` | boolean | no |  | Include scholar results |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "countries": {
      "type": "string",
      "description": "Jurisdiction filter \u2014 ISO 3166-1 alpha-2 codes, comma separated (e.g. 'US,DE'). Defaults to the run's market when one was stated."
    },
    "language": {
      "type": "string",
      "description": "Patent language NAME, not a code \u2014 e.g. 'ENGLISH', 'SWEDISH'. Comma-separate for several."
    },
    "num": {
      "type": "integer",
      "description": "Number of results to return",
      "minimum": 1,
      "maximum": 100
    },
    "scholar": {
      "type": "boolean",
      "description": "Include scholar results"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `summary`, `pagination`

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
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `search_information.total_pages` | integer |  |
| `search_information.page_number` | integer |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].rank` | integer |  |
| `organic_results[].patent_id` | string |  |
| `organic_results[].title` | string |  |
| `organic_results[].snippet` | string |  |
| `organic_results[].priority_date` | string |  |
| `organic_results[].filing_date` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_BZAYNyvAW2i3qj8X9eo93VJQ",
    "status": "Success",
    "created_at": "2026-03-28T20:43:57Z",
    "request_time_taken": 1.49,
    "parsing_time_taken": 0.0,
    "total_time_taken": 1.49,
    "request_url": "https://patents.google.com/?q=instagram.com",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_BZAYNyvAW2i3qj8X9eo93VJQ.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_BZAYNyvAW2i3qj8X9eo93VJQ"
  },
  "search_p
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

**Chain groups:** `searchapi_patents`

## Alternatives

- `serpapi_google_patents`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
