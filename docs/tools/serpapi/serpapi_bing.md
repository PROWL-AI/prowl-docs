---
name: serpapi_bing
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_bing`

Bing Web Search via SerpAPI.

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
  "tool_name": "serpapi_bing",
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
| `cc` | string | no |  | Country code |
| `mkt` | string | no |  | Market code (e.g. 'en-us') |
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
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'Austin, Texas')"
    },
    "cc": {
      "type": "string",
      "description": "Country code"
    },
    "mkt": {
      "type": "string",
      "description": "Market code (e.g. 'en-us')"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.bing_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.q` | string |  |
| `search_parameters.device` | string |  |
| `search_parameters.engine` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].tracking_link` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].displayed_link` | string |  |
| `organic_results[].thumbnail` | string |  |
| `organic_results[].snippet` | string |  |
| `pagination` | object |  |
| `pagination.current` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8602706a1f7fd3a77a",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/B1odZO15y7U5uwxuizLAoQ/69c83d8602706a1f7fd3a77a.json",
    "created_at": "2026-03-28 20:43:50 UTC",
    "processed_at": "2026-03-28 20:43:50 UTC",
    "bing_url": "https://www.bing.com/search?q=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/B1odZO15y7U5uwxuizLAoQ/69c83d8602706a1f7fd3a77a.html",
    "total_time_taken": 22.39
  },
  "search_
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

- `bing_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
