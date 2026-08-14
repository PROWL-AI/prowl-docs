---
name: airbnb_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `airbnb_search`

Airbnb Search — search vacation rentals by location and dates.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "airbnb_search",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Location (e.g. 'Paris, France') |
| `check_in_date` | string | no |  | Check-in date (YYYY-MM-DD) |
| `check_out_date` | string | no |  | Check-out date (YYYY-MM-DD) |
| `adults` | integer | no |  | Number of adults |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |
| `next_page_token` | string | no |  | Pagination token for the next page of results |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Location (e.g. 'Paris, France')"
    },
    "check_in_date": {
      "type": "string",
      "description": "Check-in date (YYYY-MM-DD)"
    },
    "check_out_date": {
      "type": "string",
      "description": "Check-out date (YYYY-MM-DD)"
    },
    "adults": {
      "type": "integer",
      "description": "Number of adults",
      "minimum": 1,
      "maximum": 9
    },
    "currency": {
      "type": "string",
      "description": "Currency code (e.g. 'USD', 'EUR')"
    },
    "next_page_token": {
      "type": "string",
      "description": "Pagination token for the next page of results"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `properties`, `pagination`

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
| `search_parameters.airbnb_domain` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.time_period` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.results` | string |  |
| `search_information.time_period` | string |  |
| `search_information.guests` | string |  |
| `properties[]` | array<object> |  |
| `properties[].position` | integer |  |
| `properties[].id` | string |  |
| `properties[].title` | string |  |
| `properties[].description` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_8A9g6Ov07XH89brrx4JlbW2m",
    "status": "Success",
    "created_at": "2026-03-28T20:44:21Z",
    "request_time_taken": 0.73,
    "parsing_time_taken": 0.02,
    "total_time_taken": 0.76,
    "request_url": "https://www.airbnb.com/s/instagram.com/homes?flexible_trip_lengths%5B%5D=one_week",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_8A9g6Ov07XH89brrx4JlbW2m.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_8A9
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

- Engine-specific SearchAPI surface — pass marketplace/locale params when the schema exposes them
- ID-like params (property_id, asin, place_id) must be real identifiers from a prior search tool

## Alternatives

- `amazon_search`
- `baidu_search`
- `bing_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
