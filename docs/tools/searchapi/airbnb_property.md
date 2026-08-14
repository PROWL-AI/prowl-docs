---
name: airbnb_property
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `airbnb_property`

Airbnb Property — detailed listing info with amenities, pricing, and host details.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "airbnb_property",
  "params": {
    "property_id": "12345678"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `property_id` | string | yes |  | Airbnb property ID |
| `check_in_date` | string | no |  | Check-in date (YYYY-MM-DD) |
| `check_out_date` | string | no |  | Check-out date (YYYY-MM-DD) |
| `adults` | integer | no |  | Number of adults |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "property_id": {
      "type": "string",
      "description": "Airbnb property ID"
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
    }
  },
  "required": [
    "property_id"
  ]
}
```

## Example request

```json
{
  "property_id": "12345678"
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
| `search_parameters.airbnb_domain` | string |  |
| `search_parameters.property_id` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_mpO7djkNqos8Yb6A2vAPE9xq",
    "status": "Success",
    "created_at": "2026-03-28T20:44:22Z",
    "request_time_taken": 0.39,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.39,
    "request_url": "https://www.airbnb.com/rooms/100",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_mpO7djkNqos8Yb6A2vAPE9xq.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_mpO7djkNqos8Yb6A2vAPE9xq"
  },
  "search_parameters":
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

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'airbnb_search', 'extract': '?'}`

## Alternatives

_None listed._

## Provider docs

https://www.searchapi.io/docs
