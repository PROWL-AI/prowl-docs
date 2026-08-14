---
name: google_ads_transparency_advertiser_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_ads_transparency_advertiser_search`

Google Ads Transparency Advertiser Search — search for advertisers by keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `google`, `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_ads_transparency_advertiser_search",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Keyword to search for advertisers or domains |
| `region` | string | no |  | Region filter (default 'anywhere') |
| `num_domains` | integer | no |  | Number of domains to return (max 100) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Keyword to search for advertisers or domains"
    },
    "region": {
      "type": "string",
      "description": "Region filter (default 'anywhere')"
    },
    "num_domains": {
      "type": "integer",
      "description": "Number of domains to return (max 100)",
      "minimum": 1,
      "maximum": 100
    }
  },
  "required": [
    "query"
  ]
}
```

## Example request

```json
{
  "query": "example query"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `advertisers`, `domains`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.request_time_taken` | number |  |
| `search_metadata.parsing_time_taken` | number |  |
| `search_metadata.total_time_taken` | number |  |
| `search_metadata.request_url` | null |  |
| `search_metadata.html_url` | string |  |
| `search_metadata.json_url` | string |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.region` | string |  |
| `search_parameters.num_advertisers` | integer |  |
| `search_parameters.num_domains` | integer |  |
| `advertisers[]` | array<object> |  |
| `advertisers[].name` | string |  |
| `advertisers[].id` | string |  |
| `advertisers[].region` | string |  |
| `advertisers[].ads_count` | object |  |
| `domains[]` | array<object> |  |
| `domains[].name` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_MG6OPWeEVjFx9Am794jR8w7N",
    "status": "Success",
    "created_at": "2026-03-28T20:43:36Z",
    "request_time_taken": 0.45,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.45,
    "request_url": null,
    "html_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9Am794jR8w7N.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9Am794jR8w7N"
  },
  "search_parameters": {
    "engine": "google_ads_t
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

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

**Chain groups:** `searchapi_ads_transparency`

## Alternatives

- `dataforseo_kw_google_ads_search_volume`
- `google_flights_location_search`
- `google_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
