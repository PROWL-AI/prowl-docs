---
name: apple_app_store
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `apple_app_store`

Apple App Store — search iOS/macOS apps by name or keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "apple_app_store",
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
| `lang` | string | no | `en` | Language code (default 'en') |
| `country` | string | no |  | Store country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "lang": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "country": {
      "type": "string",
      "description": "Store country code (e.g. 'us', 'gb')"
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

Top-level keys: `search_metadata`, `search_parameters`, `organic_results`

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
| `search_parameters.term` | string |  |
| `search_parameters.include_explicit` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.lang` | string |  |
| `search_parameters.device` | string |  |
| `search_parameters.num` | integer |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].id` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].bundle_id` | string |  |
| `organic_results[].version` | string |  |
| `organic_results[].has_vpp_license` | boolean |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_J70QVB41KphBXKwjmkqLy9mx",
    "status": "Success",
    "created_at": "2026-03-28T20:44:09Z",
    "request_time_taken": 1.55,
    "parsing_time_taken": 0.0,
    "total_time_taken": 1.56,
    "request_url": null,
    "html_url": "https://www.searchapi.io/api/v1/searches/search_J70QVB41KphBXKwjmkqLy9mx.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_J70QVB41KphBXKwjmkqLy9mx"
  },
  "search_parameters": {
    "engine": "apple_app_st
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

**Chain groups:** `searchapi_appstores`, `dataforseo_labs_appstore`

## Alternatives

- `serpapi_apple_app_store`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
