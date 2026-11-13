---
name: google_maps_directions
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-11-13T04:17:33Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_maps_directions`

Google Maps Directions — route data for driving, transit, walking, cycling, and flying with step-by-step directions and coordinates.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `maps`, `searchapi` |
| Last schema check | `PASS` — 2026-11-12T02:56:36Z |
| Last live API check | `PASS` — 2026-11-12T02:56:36.486392 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_maps_directions",
  "params": {
    "destination": "example",
    "origin": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `origin` | string | yes |  | Starting point: address, data ID, or coordinates (lat,long). Mapped to 'from' in the API request. |
| `destination` | string | yes |  | Destination: address, data ID, or coordinates (lat,long). Mapped to 'to' in the API request. |
| `travel_mode` | enum(best, driving, transit, walking, cycling, flying) | no |  | Mode of travel |
| `hl` | string | no |  | Language code |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "origin": {
      "type": "string",
      "description": "Starting point: address, data ID, or coordinates (lat,long). Mapped to 'from' in the API request."
    },
    "destination": {
      "type": "string",
      "description": "Destination: address, data ID, or coordinates (lat,long). Mapped to 'to' in the API request."
    },
    "travel_mode": {
      "type": "string",
      "description": "Mode of travel",
      "enum": [
        "best",
        "driving",
        "transit",
        "walking",
        "cycling",
        "flying"
      ]
    },
    "hl": {
      "type": "string",
      "description": "Language code",
      "pattern": "^[A-Za-z]{2,3}(?:[-_][A-Za-z0-9]{2,4})?$"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')",
      "pattern": "^[A-Za-z]{2}$"
    }
  },
  "required": [
    "origin",
    "destination"
  ]
}
```

## Example request

```json
{
  "destination": "example",
  "origin": "example"
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
  "error": "Missing required parameter from."
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

- `serpapi_google_maps_directions`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs/google
