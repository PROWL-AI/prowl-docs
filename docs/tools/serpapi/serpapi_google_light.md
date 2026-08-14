---
name: serpapi_google_light
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_light`

Google Light via SerpAPI — fast essential results, lower cost.

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
  "tool_name": "serpapi_google_light",
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
| `num` | integer | no |  | Number of results to return |

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
    },
    "num": {
      "type": "integer",
      "description": "Number of results to return",
      "minimum": 1,
      "maximum": 100
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `knowledge_graph`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_light_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.google_domain` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.organic_results_state` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].displayed_link` | string |  |
| `organic_results[].snippet` | string |  |
| `organic_results[].sitelinks` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d7765f7014e0d17e808",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/WNsNbTkMrpO3hO2jSV_nhg/69c83d7765f7014e0d17e808.json",
    "created_at": "2026-03-28 20:43:35 UTC",
    "processed_at": "2026-03-28 20:43:35 UTC",
    "google_light_url": "https://www.google.com/search?q=instagram.com&oq=instagram.com&hl=en&sourceid=chrome&ie=UTF-8&gbv=1",
    "raw_html_file": "https://serpapi.com/searches/WNsNbTkMrpO3hO2jSV_nhg/69c83d7765f70
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

- `google_light`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
