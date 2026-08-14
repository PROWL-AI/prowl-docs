---
name: google_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_search`

Google Web Search via SearchAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `google`, `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_search",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `uule` | string | no |  | Google-encoded location. Cannot be combined with `location`. |
| `lr` | string | no |  | Restrict results by language, e.g. 'lang_de' (pipe-separated for several). |
| `cr` | string | no |  | Restrict results by country of origin, e.g. 'countryDE'. |
| `safe` | enum(active, off) | no |  | SafeSearch level. |
| `filter` | integer | no |  | 1 enables Google's similar/omitted-results filters, 0 disables them. |
| `nfpr` | integer | no |  | 1 excludes auto-corrected results, 0 includes them. |
| `time_period` | string | no |  | Freshness window, e.g. 'last_day', 'last_week', 'last_month', 'last_year'. |
| `time_period_min` | string | no |  | Start of a custom freshness window (MM/DD/YYYY). |
| `time_period_max` | string | no |  | End of a custom freshness window (MM/DD/YYYY). |
| `q` | string | yes |  | Search query |
| `device` | enum(desktop, mobile) | no |  | Device type |
| `location` | string | no |  | Location for geo-targeted results (e.g. 'New York, NY') |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `num` | integer | no |  | Number of results to return |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "uule": {
      "type": "string",
      "description": "Google-encoded location. Cannot be combined with `location`."
    },
    "lr": {
      "type": "string",
      "description": "Restrict results by language, e.g. 'lang_de' (pipe-separated for several)."
    },
    "cr": {
      "type": "string",
      "description": "Restrict results by country of origin, e.g. 'countryDE'."
    },
    "safe": {
      "type": "string",
      "description": "SafeSearch level.",
      "enum": [
        "active",
        "off"
      ]
    },
    "filter": {
      "type": "integer",
      "description": "1 enables Google's similar/omitted-results filters, 0 disables them."
    },
    "nfpr": {
      "type": "integer",
      "description": "1 excludes auto-corrected results, 0 includes them."
    },
    "time_period": {
      "type": "string",
      "description": "Freshness window, e.g. 'last_day', 'last_week', 'last_month', 'last_year'."
    },
    "time_period_min": {
      "type": "string",
      "description": "Start of a custom freshness window (MM/DD/YYYY)."
    },
    "time_period_max": {
      "type": "string",
      "description": "End of a custom freshness window (MM/DD/YYYY)."
    },
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "device": {
      "type": "string",
      "description": "Device type",
      "enum": [
        "desktop",
        "mobile"
      ]
    },
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'New York, NY')"
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
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `related_questions`, `pagination`

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
| `search_parameters.device` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.time_taken_displayed` | number |  |
| `search_information.detected_location` | string |  |
| `search_information.has_no_results_for` | boolean |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].title` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_WDz0ZKeWNOc29ZmLxkQyABpo",
    "status": "Success",
    "created_at": "2026-03-28T20:43:35Z",
    "request_time_taken": 2.33,
    "parsing_time_taken": 0.03,
    "total_time_taken": 2.36,
    "request_url": "https://www.google.com/search?q=instagram.com&oq=instagram.com&gl=us&hl=en&ie=UTF-8",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_WDz0ZKeWNOc29ZmLxkQyABpo.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_W
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

## Alternatives

- `exa_keyword_search`
- `dataforseo_serp_google_organic`
- `serpapi_google`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
