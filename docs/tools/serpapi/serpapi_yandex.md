---
name: serpapi_yandex
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_yandex`

Yandex Web Search via SerpAPI — Russian search engine.

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
  "tool_name": "serpapi_yandex",
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
| `lr` | string | no |  | Region code |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "lr": {
      "type": "string",
      "description": "Region code"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.yandex_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.text` | string |  |
| `search_parameters.engine` | string |  |
| `search_parameters.lang` | string |  |
| `search_parameters.lr` | string |  |
| `search_parameters.yandex_domain` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `search_information.query_displayed` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].displayed_link` | string |  |
| `organic_results[].snippet` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8a7bf2f9981861fd3e",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/xT00lJ_rniaYsqzJw8JXxw/69c83d8a7bf2f9981861fd3e.json",
    "created_at": "2026-03-28 20:43:54 UTC",
    "processed_at": "2026-03-28 20:43:54 UTC",
    "yandex_url": "https://yandex.com/search/?lang=en&lr=84&text=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/xT00lJ_rniaYsqzJw8JXxw/69c83d8a7bf2f9981861fd3e.html",
    "total_time_taken": 1.6
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

- `yandex_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
