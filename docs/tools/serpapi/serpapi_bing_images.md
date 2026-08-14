---
name: serpapi_bing_images
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_bing_images`

Bing Images search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_bing_images",
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
| `mkt` | string | no |  | Market code |
| `safeSearch` | enum(Off, Moderate, Strict) | no |  | Safe search filter |
| `count` | integer | no |  | Number of results |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "mkt": {
      "type": "string",
      "description": "Market code"
    },
    "safeSearch": {
      "type": "string",
      "description": "Safe search filter",
      "enum": [
        "Off",
        "Moderate",
        "Strict"
      ]
    },
    "count": {
      "type": "integer",
      "description": "Number of results",
      "minimum": 1,
      "maximum": 50
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

Top-level keys: `search_metadata`, `search_parameters`, `images_results`, `suggested_searches`, `related_searches`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.bing_images_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.device` | string |  |
| `images_results[]` | array<object> |  |
| `images_results[].thumbnail` | string |  |
| `images_results[].link` | string |  |
| `images_results[].title` | string |  |
| `images_results[].size` | string |  |
| `images_results[].source` | string |  |
| `images_results[].domain` | string |  |
| `images_results[].source_logo` | string |  |
| `images_results[].original` | string |  |
| `images_results[].description` | string |  |
| `images_results[].position` | integer |  |
| `suggested_searches[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d87a6885593af600953",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/NNOhXw7blzC51asQvIMztA/69c83d87a6885593af600953.json",
    "created_at": "2026-03-28 20:43:51 UTC",
    "processed_at": "2026-03-28 20:43:51 UTC",
    "bing_images_url": "https://www.bing.com/images/search?q=instagram.com&qft=",
    "raw_html_file": "https://serpapi.com/searches/NNOhXw7blzC51asQvIMztA/69c83d87a6885593af600953.html",
    "total_time_taken": 0.
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

- `bing_images`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
