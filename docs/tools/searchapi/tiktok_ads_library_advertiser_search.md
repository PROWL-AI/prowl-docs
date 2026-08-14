---
name: tiktok_ads_library_advertiser_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `tiktok_ads_library_advertiser_search`

TikTok Ads Library Advertiser Search — find TikTok advertisers by name.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `search`, `searchapi`, `tiktok` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "tiktok_ads_library_advertiser_search",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Advertiser name |
| `country_code` | string | no |  | Country code |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Advertiser name"
    },
    "country_code": {
      "type": "string",
      "description": "Country code"
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
| `search_parameters.q` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_WDz0ZKeWNOc29ZV6rkQyABpo",
    "status": "Success",
    "created_at": "2026-03-28T20:44:01Z",
    "request_time_taken": 0.43,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.43,
    "request_url": "https://library.tiktok.com/ads",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_WDz0ZKeWNOc29ZV6rkQyABpo.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_WDz0ZKeWNOc29ZV6rkQyABpo"
  },
  "search_parameters": {
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

- Engine-specific SearchAPI surface — pass marketplace/locale params when the schema exposes them
- ID-like params (property_id, asin, place_id) must be real identifiers from a prior search tool

## Alternatives

- `google_ads_transparency_advertiser_search`
- `meta_ad_library_page_search`
- `tiktok_ads_library`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
