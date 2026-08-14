---
name: serpapi_google_local
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_local`

Google Local results via SerpAPI — businesses and places near a location.

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
  "tool_name": "serpapi_google_local",
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
| `location` | string | no |  | Location for geo-targeted results (e.g. 'Austin, Texas') |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'Austin, Texas')"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
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

Top-level keys: `search_metadata`, `search_parameters`, `local_map`, `local_results`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_local_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.google_domain` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.device` | string |  |
| `local_map` | object |  |
| `local_map.gps_coordinates` | object |  |
| `local_map.gps_coordinates.latitude` | number |  |
| `local_map.gps_coordinates.longitude` | number |  |
| `local_results[]` | array<object> |  |
| `local_results[].position` | integer |  |
| `local_results[].rating` | number |  |
| `local_results[].reviews` | integer |  |
| `local_results[].reviews_original` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d785b92f818de8becd3",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/JuXYusQrm2R4-QkNziL-vg/69c83d785b92f818de8becd3.json",
    "created_at": "2026-03-28 20:43:36 UTC",
    "processed_at": "2026-03-28 20:43:36 UTC",
    "google_local_url": "https://www.google.com/search?q=instagram.com&hl=en&gl=us&udm=1",
    "raw_html_file": "https://serpapi.com/searches/JuXYusQrm2R4-QkNziL-vg/69c83d785b92f818de8becd3.html",
    "total_time_t
...
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

- `google_local`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
