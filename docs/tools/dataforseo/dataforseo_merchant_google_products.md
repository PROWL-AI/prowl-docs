---
name: dataforseo_merchant_google_products
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_merchant_google_products`

Search Google Shopping products — get product listings, prices, ratings, and seller info.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `dataforseo`, `google` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_merchant_google_products",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `language_code` | string | no |  | language code |
| `location_code` | integer | no |  | location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `max_crawl_pages` | integer | no |  | page crawl limit |
| `pingback_url` | string | no |  | notification URL of a completed task |
| `postback_data` | string | no |  | postback_url datatype |
| `postback_url` | string | no |  | URL for sending task results |
| `priority` | integer | no |  | task priority |
| `se_domain` | string | no |  | search engine domain |
| `search_param` | string | no |  | additional parameters of the search query |
| `tag` | string | no |  | user-defined task identifier |
| `url` | string | no |  | direct URL of the search query |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `depth` | integer | no |  | Number of results to return (max 120) |
| `price_min` | number | no |  |  |
| `price_max` | number | no |  |  |
| `sort_by` | string | no |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "language_code": {
      "type": "string",
      "description": "language code"
    },
    "location_code": {
      "type": "integer",
      "description": "location code"
    },
    "location_coordinate": {
      "type": "string",
      "description": "GPS coordinates of a location"
    },
    "max_crawl_pages": {
      "type": "integer",
      "description": "page crawl limit"
    },
    "pingback_url": {
      "type": "string",
      "description": "notification URL of a completed task"
    },
    "postback_data": {
      "type": "string",
      "description": "postback_url datatype"
    },
    "postback_url": {
      "type": "string",
      "description": "URL for sending task results"
    },
    "priority": {
      "type": "integer",
      "description": "task priority"
    },
    "se_domain": {
      "type": "string",
      "description": "search engine domain"
    },
    "search_param": {
      "type": "string",
      "description": "additional parameters of the search query"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
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
    "depth": {
      "type": "integer",
      "description": "Number of results to return (max 120)",
      "minimum": 1,
      "maximum": 120
    },
    "price_min": {
      "type": "number"
    },
    "price_max": {
      "type": "number"
    },
    "sort_by": {
      "type": "string"
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
| `tasks[].data.keyword` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].data.se_type` | string |  |
| `tasks[].data.se` | string |  |
| `tasks[].data.device` | string |  |
| `tasks[].data.os` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0118 sec.",
  "cost": 0.001,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0179-0000-9f68d8b2c087",
      "status_code": 20100,
      "status_message": "Task Created.",
      "time": "0.0040 sec.",
      "cost": 0.001,
      "result_count": 0,
      "path": [
        "v3",
        "merchant",
        "google",
        "products",
        "task_post"
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

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

**Chain groups:** `dataforseo_merchant`

## Alternatives

- `dataforseo_app_google_info`
- `dataforseo_app_google_searches`
- `dataforseo_serp_google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
