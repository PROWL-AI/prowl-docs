---
name: serpapi_tripadvisor
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_tripadvisor`

Tripadvisor search via SerpAPI — hotels, restaurants, attractions.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_tripadvisor",
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
| `location_id` | string | no |  | Tripadvisor location ID |
| `tripadvisor_domain` | string | no |  | Regional Tripadvisor site, e.g. 'www.tripadvisor.co.uk'. SerpApi requires the www. prefix (a bare 'tripadvisor.co.uk' returns HTTP 400); it is added for you if omitted. Defaults to www.tripadvisor.com. |
| `lat` | number | no |  | Latitude of the search origin. |
| `lon` | number | no |  | Longitude of the search origin. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "location_id": {
      "type": "string",
      "description": "Tripadvisor location ID"
    },
    "tripadvisor_domain": {
      "type": "string",
      "description": "Regional Tripadvisor site, e.g. 'www.tripadvisor.co.uk'. SerpApi requires the www. prefix (a bare 'tripadvisor.co.uk' returns HTTP 400); it is added for you if omitted. Defaults to www.tripadvisor.com."
    },
    "lat": {
      "type": "number",
      "description": "Latitude of the search origin."
    },
    "lon": {
      "type": "number",
      "description": "Longitude of the search origin."
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

Top-level keys: `search_metadata`, `search_parameters`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.tripadvisor_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.tripadvisor_domain` | string |  |
| `search_parameters.ssrc` | string |  |
| `search_parameters.offset` | integer |  |
| `search_parameters.limit` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8e5e3494f292968cf0",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/V1Cf9VPqKbMFVS99ed9n3w/69c83d8e5e3494f292968cf0.json",
    "created_at": "2026-03-28 20:43:58 UTC",
    "processed_at": "2026-03-28 20:43:58 UTC",
    "tripadvisor_url": "https://www.tripadvisor.com/Search?q=instagram.com&ssrc=a&geo=1&offset=0&limit=30",
    "raw_html_file": "https://serpapi.com/searches/V1Cf9VPqKbMFVS99ed9n3w/69c83d8e5e3494f292968cf0.html",

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

**Chain groups:** `serpapi_places`

## Alternatives

- `tripadvisor_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
