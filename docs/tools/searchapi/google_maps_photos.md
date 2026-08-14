---
name: google_maps_photos
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_maps_photos`

Google Maps Photos — photos for a place with category filtering and pagination.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `maps`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_maps_photos",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `place_id` | string | no |  | Google Maps place ID |
| `data_id` | string | no |  | Google Maps data ID |
| `category_id` | string | no |  | Photo category ID to filter by |
| `next_page_token` | string | no |  | Pagination token for next page |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "place_id": {
      "type": "string",
      "description": "Google Maps place ID"
    },
    "data_id": {
      "type": "string",
      "description": "Google Maps data ID"
    },
    "category_id": {
      "type": "string",
      "description": "Photo category ID to filter by"
    },
    "next_page_token": {
      "type": "string",
      "description": "Pagination token for next page"
    }
  },
  "required": []
}
```

## Example request

```json
{}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Missing required parameter: either place_id or data_id"
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

- `google_maps`
- `google_maps_directions`
- `google_maps_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
