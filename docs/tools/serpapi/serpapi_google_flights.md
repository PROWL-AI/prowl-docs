---
name: serpapi_google_flights
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_flights`

Google Flights search via SerpAPI — flight prices and options.

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
  "tool_name": "serpapi_google_flights",
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
| `departure_id` | string | yes |  | Departure airport IATA code (e.g. 'JFK') |
| `arrival_id` | string | yes |  | Arrival airport IATA code (e.g. 'LAX') |
| `outbound_date` | string | yes |  | Outbound date (YYYY-MM-DD) |
| `return_date` | string | no |  | Return date (YYYY-MM-DD) for round-trip |
| `type` | integer | no |  | 1=round-trip, 2=one-way |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "departure_id": {
      "type": "string",
      "description": "Departure airport IATA code (e.g. 'JFK')"
    },
    "arrival_id": {
      "type": "string",
      "description": "Arrival airport IATA code (e.g. 'LAX')"
    },
    "outbound_date": {
      "type": "string",
      "description": "Outbound date (YYYY-MM-DD)"
    },
    "return_date": {
      "type": "string",
      "description": "Return date (YYYY-MM-DD) for round-trip"
    },
    "type": {
      "type": "integer",
      "description": "1=round-trip, 2=one-way"
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
  "error": "`return_date` is required if `type` is `1` (Round trip)."
}
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

- `google_flights`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
