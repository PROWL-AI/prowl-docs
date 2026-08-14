---
name: google_hotels
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_hotels`

Google Hotels — search hotels with pricing, ratings, and amenities.

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
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_hotels",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Location or hotel name |
| `check_in_date` | string | no |  | Check-in date (YYYY-MM-DD) |
| `check_out_date` | string | no |  | Check-out date (YYYY-MM-DD) |
| `adults` | integer | no |  | Number of adults |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |
| `sort_by` | enum(lowest_price, highest_rating) | no |  | Sort by |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Location or hotel name"
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
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    },
    "currency": {
      "type": "string",
      "description": "Currency code (e.g. 'USD', 'EUR')"
    },
    "sort_by": {
      "type": "string",
      "description": "Sort by",
      "enum": [
        "lowest_price",
        "highest_rating"
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
| `search_parameters.check_in_date` | string |  |
| `search_parameters.check_out_date` | string |  |
| `search_parameters.currency` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.adults` | integer |  |
| `search_parameters.property_type` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_MG6OPWeEVjFx9Ary74jR8w7N",
    "status": "Success",
    "created_at": "2026-03-28T20:43:58Z",
    "request_time_taken": 0.68,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.68,
    "request_url": "https://www.google.com/travel/search?q=instagram.com",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9Ary74jR8w7N.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9Ary74jR8w7N"
  },
  
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

- `serpapi_google_hotels`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
