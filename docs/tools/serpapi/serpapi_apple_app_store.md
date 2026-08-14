---
name: serpapi_apple_app_store
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_apple_app_store`

Apple App Store search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_apple_app_store",
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
| `country` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "country": {
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.apple_app_store_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.term` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.lang` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `search_information.results_count` | integer |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].id` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].bundle_id` | string |  |
| `organic_results[].version` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8dbd1731025b6e51a9",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/JrNyGXU2Ax5deAnGg-mVCA/69c83d8dbd1731025b6e51a9.json",
    "created_at": "2026-03-28 20:43:57 UTC",
    "processed_at": "2026-03-28 20:43:57 UTC",
    "apple_app_store_url": "https://itunes.apple.com/search?media=software&term=instagram.com&country=us&lang=en-us&explicit=yes",
    "raw_html_file": "https://serpapi.com/searches/JrNyGXU2Ax5deAnGg-mVCA/69c83d8db
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

**Chain groups:** `serpapi_apple`

## Alternatives

- `apple_app_store`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
