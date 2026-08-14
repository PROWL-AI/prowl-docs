---
name: google_flights
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_flights`

Google Flights — search flights between airports/cities with dates, class, and stops filtering.

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
  "tool_name": "google_flights",
  "params": {
    "arrival_id": "arrival_id_example",
    "departure_id": "departure_id_example",
    "outbound_date": "YYYY-MM-DD"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `departure_id` | string | yes |  | Departure airport/city code (e.g. 'JFK', 'LAX') |
| `arrival_id` | string | yes |  | Arrival airport/city code |
| `outbound_date` | string | yes |  | Outbound date (YYYY-MM-DD) |
| `return_date` | string | no |  | Return date for round trip (YYYY-MM-DD) |
| `flight_type` | enum(round_trip, one_way, multi_city) | no |  | Flight type |
| `travel_class` | enum(1, 2, 3, 4) | no |  | Travel class: 1=economy, 2=premium economy, 3=business, 4=first |
| `adults` | integer | no |  | Number of adults |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |
| `stops` | enum(0, 1, 2) | no |  | Max stops: 0=nonstop, 1=one stop, 2=two stops |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "departure_id": {
      "type": "string",
      "description": "Departure airport/city code (e.g. 'JFK', 'LAX')"
    },
    "arrival_id": {
      "type": "string",
      "description": "Arrival airport/city code"
    },
    "outbound_date": {
      "type": "string",
      "description": "Outbound date (YYYY-MM-DD)"
    },
    "return_date": {
      "type": "string",
      "description": "Return date for round trip (YYYY-MM-DD)"
    },
    "flight_type": {
      "type": "string",
      "description": "Flight type",
      "enum": [
        "round_trip",
        "one_way",
        "multi_city"
      ]
    },
    "travel_class": {
      "type": "integer",
      "description": "Travel class: 1=economy, 2=premium economy, 3=business, 4=first",
      "enum": [
        1,
        2,
        3,
        4
      ]
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
    "stops": {
      "type": "integer",
      "description": "Max stops: 0=nonstop, 1=one stop, 2=two stops",
      "enum": [
        0,
        1,
        2
      ]
    }
  },
  "required": [
    "departure_id",
    "arrival_id",
    "outbound_date"
  ]
}
```

## Example request

```json
{
  "arrival_id": "arrival_id_example",
  "departure_id": "departure_id_example",
  "outbound_date": "YYYY-MM-DD"
}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Missing required parameter return_date."
}
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

- `serpapi_google_flights`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
