---
name: dataforseo_serp_google_organic
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_organic`

Get real-time Google organic SERP results via DataForSEO.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `dataforseo`, `google`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_google_organic",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `browser_screen_height` | integer | no |  | browser screen height |
| `browser_screen_resolution_ratio` | integer | no |  | browser screen resolution ratio |
| `browser_screen_width` | integer | no |  | browser screen width |
| `calculate_rectangles` | boolean | no |  | calcualte pixel rankings for SERP elements in advanced results |
| `find_targets_in` | any[] | no |  | SERP element types to check for targets |
| `group_organic_results` | boolean | no |  | display related results |
| `ignore_targets_in` | any[] | no |  | SERP element types to exclude from target search |
| `language_code` | string | no |  | search engine language code |
| `load_async_ai_overview` | boolean | no |  | load asynchronous ai overview |
| `location_code` | integer | no |  | search engine location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `match_type` | string | no |  | target match type |
| `match_value` | string | no |  | target domain, subdomain, or wildcard value |
| `max_crawl_pages` | integer | no |  | page crawl limit |
| `people_also_ask_click_depth` | integer | no |  | clicks on the corresponding element |
| `remove_from_url` | any[] | no |  | remove specific parameters from URLs |
| `se_domain` | string | no |  | search engine domain |
| `search_param` | string | no |  | additional parameters of the search query |
| `stop_crawl_on_match` | any[] | no |  | array of targets to stop crawling |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | no |  | target domain, subdomain, or webpage to get results for |
| `target_search_mode` | enum(all, any) | no |  | target matching mode |
| `url` | string | no |  | direct URL of the search query |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `device` | enum(desktop, mobile) | no |  | Device type |
| `os_type` | enum(windows, macos) | no |  | Operating system |
| `depth` | integer | no |  | Number of results to return (max 200) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "browser_screen_height": {
      "type": "integer",
      "description": "browser screen height"
    },
    "browser_screen_resolution_ratio": {
      "type": "integer",
      "description": "browser screen resolution ratio"
    },
    "browser_screen_width": {
      "type": "integer",
      "description": "browser screen width"
    },
    "calculate_rectangles": {
      "type": "boolean",
      "description": "calcualte pixel rankings for SERP elements in advanced results"
    },
    "find_targets_in": {
      "type": "array",
      "description": "SERP element types to check for targets"
    },
    "group_organic_results": {
      "type": "boolean",
      "description": "display related results"
    },
    "ignore_targets_in": {
      "type": "array",
      "description": "SERP element types to exclude from target search"
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "load_async_ai_overview": {
      "type": "boolean",
      "description": "load asynchronous ai overview"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "location_coordinate": {
      "type": "string",
      "description": "GPS coordinates of a location"
    },
    "match_type": {
      "type": "string",
      "description": "target match type"
    },
    "match_value": {
      "type": "string",
      "description": "target domain, subdomain, or wildcard value"
    },
    "max_crawl_pages": {
      "type": "integer",
      "description": "page crawl limit"
    },
    "people_also_ask_click_depth": {
      "type": "integer",
      "description": "clicks on the corresponding element"
    },
    "remove_from_url": {
      "type": "array",
      "description": "remove specific parameters from URLs"
    },
    "se_domain": {
      "type": "string",
      "description": "search engine domain"
    },
    "search_param": {
      "type": "string",
      "description": "additional parameters of the search query"
    },
    "stop_crawl_on_match": {
      "type": "array",
      "description": "array of targets to stop crawling"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "target": {
      "type": "string",
      "description": "target domain, subdomain, or webpage to get results for"
    },
    "target_search_mode": {
      "type": "string",
      "description": "target matching mode",
      "enum": [
        "all",
        "any"
      ]
    },
    "url": {
      "type": "string",
      "description": "direct URL of the search query"
    },
    "keyword": {
      "type": "string",
      "description": "Search keyword or query"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "device": {
      "type": "string",
      "description": "Device type",
      "enum": [
        "desktop",
        "mobile"
      ]
    },
    "os_type": {
      "type": "string",
      "description": "Operating system",
      "enum": [
        "windows",
        "macos"
      ]
    },
    "depth": {
      "type": "integer",
      "description": "Number of results to return (max 200)",
      "minimum": 1,
      "maximum": 200
    }
  },
  "required": [
    "keyword"
  ]
}
```

## Example request

```json
{
  "keyword": "example query"
}
```

## Output

Top-level keys: `version`, `status_code`, `status_message`, `time`, `cost`, `tasks_count`, `tasks_error`, `tasks`

| Path | Type | Description |
|------|------|-------------|
| `version` | string |  |
| `status_code` | integer |  |
| `status_message` | string |  |
| `time` | string |  |
| `cost` | number |  |
| `tasks_count` | integer |  |
| `tasks_error` | integer |  |
| `tasks[]` | array<object> |  |
| `tasks[].id` | string |  |
| `tasks[].status_code` | integer |  |
| `tasks[].status_message` | string |  |
| `tasks[].time` | string |  |
| `tasks[].cost` | number |  |
| `tasks[].result_count` | integer |  |
| `tasks[].path[]` | array<string> |  |
| `tasks[].data` | object |  |
| `tasks[].data.api` | string |  |
| `tasks[].data.function` | string |  |
| `tasks[].data.se` | string |  |
| `tasks[].data.se_type` | string |  |
| `tasks[].data.keyword` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].data.device` | string |  |
| `tasks[].data.os` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "6.0758 sec.",
  "cost": 0.002,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111836-1544-0139-0000-72cfa885c60e",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "5.9312 sec.",
      "cost": 0.002,
      "result_count": 1,
      "path": [
        "v3",
        "serp",
        "google",
        "organic",
        "live",
        "advanced"
      ],
    
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- Primary tool for Google organic SERP analysis. Prefer over SearchAPI google_search when you need structured SERP features (PAA, knowledge graph, etc.) or advanced filtering.

## Alternatives

- `spyfu_serp_analysis`
- `google_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
