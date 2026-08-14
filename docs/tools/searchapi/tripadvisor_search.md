---
name: tripadvisor_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `tripadvisor_search`

Tripadvisor Search — search hotels, restaurants, and attractions.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "tripadvisor_search",
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
| `tripadvisor_domain` | string | no |  | Regional Tripadvisor site, e.g. 'tripadvisor.co.uk'. Each domain is a specific country/region AND language — without it you get the US site's view of the place. |
| `location` | string | no |  | Location to search from; the engine resolves it to coordinates. |
| `lat` | number | no |  | Latitude (-90..90). Must be given together with lon. |
| `lon` | number | no |  | Longitude (-180..180). Must be given together with lat. |
| `category` | enum(places, forums, things_to_do, restaurants, destinations, hotels, airlines) | no |  | Result category filter. |
| `num` | integer | no |  | Results per page (1-100). |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "tripadvisor_domain": {
      "type": "string",
      "description": "Regional Tripadvisor site, e.g. 'tripadvisor.co.uk'. Each domain is a specific country/region AND language \u2014 without it you get the US site's view of the place."
    },
    "location": {
      "type": "string",
      "description": "Location to search from; the engine resolves it to coordinates."
    },
    "lat": {
      "type": "number",
      "description": "Latitude (-90..90). Must be given together with lon.",
      "minimum": -90,
      "maximum": 90
    },
    "lon": {
      "type": "number",
      "description": "Longitude (-180..180). Must be given together with lat.",
      "minimum": -180,
      "maximum": 180
    },
    "category": {
      "type": "string",
      "description": "Result category filter.",
      "enum": [
        "places",
        "forums",
        "things_to_do",
        "restaurants",
        "destinations",
        "hotels",
        "airlines"
      ]
    },
    "num": {
      "type": "integer",
      "description": "Results per page (1-100).",
      "minimum": 1,
      "maximum": 100
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
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
| `search_parameters.tripadvisor_domain` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.category` | string |  |
| `search_parameters.page` | integer |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_mpKN8l48W3iEbVdZKe3n1ZDx",
    "status": "Success",
    "created_at": "2026-03-28T20:44:23Z",
    "request_time_taken": 0.44,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.44,
    "request_url": "https://www.tripadvisor.com/Search?q=instagram.com&ssrc=a&geo=1&offset=0&limit=30",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_mpKN8l48W3iEbVdZKe3n1ZDx.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_mpKN
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

- SearchAPI.io engine tool — set locale/geo params when available for market-correct results
- Use a prior search/list tool to obtain IDs before detail/reviews calls

## Alternatives

- `serpapi_tripadvisor`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
