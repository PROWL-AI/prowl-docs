---
name: bing_images
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `bing_images`

Bing Images — image search via Bing.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "bing_images",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `country_code` | string | no |  | Two-letter country code. Mutually exclusive with `market_code`. |
| `language` | string | no |  | Language code, e.g. 'de'. |
| `location` | string | no |  | Canonical location name, e.g. 'Berlin, Germany'. |
| `device` | enum(desktop, mobile) | no |  | Device type. |
| `safe_search` | enum(off, moderate, strict) | no |  | SafeSearch level (default: moderate). |
| `time_period` | string | no |  | Freshness window, e.g. 'last_day', 'last_week', 'last_month', 'last_year'. |
| `time_period_min` | string | no |  | Start of a custom freshness window (MM/DD/YYYY). |
| `time_period_max` | string | no |  | End of a custom freshness window (MM/DD/YYYY). |
| `q` | string | yes |  | Search query |
| `market_code` | string | no |  | Market code (e.g. 'en-US') |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "country_code": {
      "type": "string",
      "description": "Two-letter country code. Mutually exclusive with `market_code`."
    },
    "language": {
      "type": "string",
      "description": "Language code, e.g. 'de'."
    },
    "location": {
      "type": "string",
      "description": "Canonical location name, e.g. 'Berlin, Germany'."
    },
    "device": {
      "type": "string",
      "description": "Device type.",
      "enum": [
        "desktop",
        "mobile"
      ]
    },
    "safe_search": {
      "type": "string",
      "description": "SafeSearch level (default: moderate).",
      "enum": [
        "off",
        "moderate",
        "strict"
      ]
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
    "market_code": {
      "type": "string",
      "description": "Market code (e.g. 'en-US')"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `suggestions`, `images`, `related_searches`

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
| `search_parameters.country_code` | string |  |
| `search_parameters.safe_search` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.safe_search` | string |  |
| `suggestions[]` | array<object> |  |
| `suggestions[].title` | string |  |
| `suggestions[].link` | string |  |
| `suggestions[].thumbnail` | string |  |
| `images[]` | array<object> |  |
| `images[].position` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_DWmO1QkoEbuMGrwED4J2r8Ga",
    "status": "Success",
    "created_at": "2026-03-28T20:44:13Z",
    "request_time_taken": 0.98,
    "parsing_time_taken": 0.04,
    "total_time_taken": 1.02,
    "request_url": "https://www.bing.com/images/search?q=instagram.com&cc=US&first=1",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_DWmO1QkoEbuMGrwED4J2r8Ga.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_DWmO1QkoEbuMGrwED4J2
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

- SearchAPI.io engine tool — set locale/geo params when available for market-correct results
- Use a prior search/list tool to obtain IDs before detail/reviews calls

## Alternatives

- `serpapi_bing_images`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
