---
name: google_flights_calendar
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_flights_calendar`

Google Flights Calendar — flight price calendar showing cheapest dates to fly.

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
  "tool_name": "google_flights_calendar",
  "params": {
    "arrival_id": "arrival_id_example",
    "departure_id": "departure_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `departure_id` | string | yes |  | Departure airport/city code (e.g. 'JFK') |
| `arrival_id` | string | yes |  | Arrival airport/city code (e.g. 'MAD') |
| `outbound_date` | string | no |  | Outbound date (YYYY-MM-DD) |
| `return_date` | string | no |  | Return date (YYYY-MM-DD). Required for round_trip. |
| `flight_type` | enum(round_trip, one_way) | no |  | Flight type |
| `hl` | string | no |  | Language code |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "departure_id": {
      "type": "string",
      "description": "Departure airport/city code (e.g. 'JFK')"
    },
    "arrival_id": {
      "type": "string",
      "description": "Arrival airport/city code (e.g. 'MAD')"
    },
    "outbound_date": {
      "type": "string",
      "description": "Outbound date (YYYY-MM-DD)"
    },
    "return_date": {
      "type": "string",
      "description": "Return date (YYYY-MM-DD). Required for round_trip."
    },
    "flight_type": {
      "type": "string",
      "description": "Flight type",
      "enum": [
        "round_trip",
        "one_way"
      ]
    },
    "hl": {
      "type": "string",
      "description": "Language code"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    },
    "currency": {
      "type": "string",
      "description": "Currency code (e.g. 'USD', 'EUR')"
    }
  },
  "required": [
    "departure_id",
    "arrival_id"
  ]
}
```

## Example request

```json
{
  "arrival_id": "arrival_id_example",
  "departure_id": "departure_id_example"
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

- `google_about_this_domain`
- `google_ads_transparency_advertiser_search`
- `google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
