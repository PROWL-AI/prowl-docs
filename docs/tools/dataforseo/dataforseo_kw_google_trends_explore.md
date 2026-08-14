---
name: dataforseo_kw_google_trends_explore
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_kw_google_trends_explore`

Get Google Trends data — keyword popularity over time for Google Search, News, Images, Shopping, or YouTube.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `trends` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_kw_google_trends_explore",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `category_code` | integer | no |  | google trends search category |
| `item_types` | any[] | no |  | types of items returned |
| `language_code` | string | no |  | search engine language code |
| `location_code` | string | no |  | search engine location code |
| `tag` | string | no |  | user-defined task identifier |
| `time_range` | string | no |  | preset time ranges |
| `keywords` | string[] | yes |  | List of keywords (up to 1000) |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `trends_type` | enum(web_search, news_search, image_search, google_shopping, youtube_search) | no |  | Trends type |
| `date_from` | string | no |  | Start date (YYYY-MM-DD) |
| `date_to` | string | no |  | End date (YYYY-MM-DD) |
| `category` | integer | no |  | Google Trends category ID |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "category_code": {
      "type": "integer",
      "description": "google trends search category"
    },
    "item_types": {
      "type": "array",
      "description": "types of items returned"
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "location_code": {
      "type": "string",
      "description": "search engine location code"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "time_range": {
      "type": "string",
      "description": "preset time ranges"
    },
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of keywords (up to 1000)"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "trends_type": {
      "type": "string",
      "description": "Trends type",
      "enum": [
        "web_search",
        "news_search",
        "image_search",
        "google_shopping",
        "youtube_search"
      ]
    },
    "date_from": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD)"
    },
    "date_to": {
      "type": "string",
      "description": "End date (YYYY-MM-DD)"
    },
    "category": {
      "type": "integer",
      "description": "Google Trends category ID"
    }
  },
  "required": [
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": []
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
| `tasks[].data.keywords[]` | array<string> |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].keywords[]` | array<string> |  |
| `tasks[].result[].type` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "16.0501 sec.",
  "cost": 0.011,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0173-0000-4d9667e18bdb",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "16.0351 sec.",
      "cost": 0.011,
      "result_count": 1,
      "path": [
        "v3",
        "keywords_data",
        "google_trends",
        "explore",
        "live"
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

## Alternatives

- `dataforseo_kw_dataforseo_trends_explore`
- `google_trends`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
