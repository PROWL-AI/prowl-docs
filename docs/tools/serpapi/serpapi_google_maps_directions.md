---
name: serpapi_google_maps_directions
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_maps_directions`

Google Maps Directions via SerpAPI — routing between two locations.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `maps`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_maps_directions",
  "params": {
    "end_addr": "example",
    "start_addr": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `start_addr` | string | yes |  | Address of the route's starting point |
| `end_addr` | string | yes |  | Address of the route's destination |
| `start_coords` | string | no |  | Optional. Starting point as 'latitude,longitude', instead of an address. |
| `end_coords` | string | no |  | Optional. Destination as 'latitude,longitude', instead of an address. |
| `travel_mode` | enum(0, 1, 2, 3, 4, 6, 9) | no |  | Travel mode: 6 best (default), 0 driving, 9 two-wheeler, 3 transit, 2 walking, 1 cycling, 4 flight. |
| `gl` | string | no |  | Country for the search, ISO alpha-2. Defaults to the run's market when one was stated. |
| `hl` | string | no | `en` | Language code (default 'en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "start_addr": {
      "type": "string",
      "description": "Address of the route's starting point"
    },
    "end_addr": {
      "type": "string",
      "description": "Address of the route's destination"
    },
    "start_coords": {
      "type": "string",
      "description": "Optional. Starting point as 'latitude,longitude', instead of an address."
    },
    "end_coords": {
      "type": "string",
      "description": "Optional. Destination as 'latitude,longitude', instead of an address."
    },
    "travel_mode": {
      "type": "integer",
      "description": "Travel mode: 6 best (default), 0 driving, 9 two-wheeler, 3 transit, 2 walking, 1 cycling, 4 flight.",
      "enum": [
        0,
        1,
        2,
        3,
        4,
        6,
        9
      ]
    },
    "gl": {
      "type": "string",
      "description": "Country for the search, ISO alpha-2. Defaults to the run's market when one was stated."
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    }
  },
  "required": [
    "start_addr",
    "end_addr"
  ]
}
```

## Example request

```json
{
  "end_addr": "example",
  "start_addr": "example"
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
  "error": "At least one of `start_addr`, `start_data_id` and `start_coords` should be set."
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

- `google_maps_directions`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
