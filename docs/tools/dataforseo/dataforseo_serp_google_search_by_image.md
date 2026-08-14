---
name: dataforseo_serp_google_search_by_image
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_search_by_image`

Create a Google reverse image search task (async) via Google Lens — find pages containing a specific image.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | 150.0 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `search`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_google_search_by_image",
  "params": {
    "image_url": "https://example.com"
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
| `calculate_rectangles` | boolean | no |  | calculate pixel rankings for SERP elements in advanced results |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `max_crawl_pages` | integer | no |  | page crawl limit |
| `postback_data` | string | no |  | postback_url datatype |
| `priority` | integer | no |  | task priority |
| `se_domain` | string | no |  | search engine domain |
| `search_param` | string | no |  | additional parameters of the search query |
| `image_url` | string | yes |  | URL of the image to search for |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `pingback_url` | string | no |  | Notification URL when task is ready |
| `postback_url` | string | no |  | URL to receive results when ready |
| `tag` | string | no |  | User-defined task tag |

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
      "description": "calculate pixel rankings for SERP elements in advanced results"
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "location_coordinate": {
      "type": "string",
      "description": "GPS coordinates of a location"
    },
    "max_crawl_pages": {
      "type": "integer",
      "description": "page crawl limit"
    },
    "postback_data": {
      "type": "string",
      "description": "postback_url datatype"
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
    "image_url": {
      "type": "string",
      "description": "URL of the image to search for"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "pingback_url": {
      "type": "string",
      "description": "Notification URL when task is ready"
    },
    "postback_url": {
      "type": "string",
      "description": "URL to receive results when ready"
    },
    "tag": {
      "type": "string",
      "description": "User-defined task tag"
    }
  },
  "required": [
    "image_url"
  ]
}
```

## Example request

```json
{
  "image_url": "https://example.com"
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
| `tasks[].data.image_url` | string |  |
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
  "time": "0.0174 sec.",
  "cost": 0.0006,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0066-0000-561eb73e4377",
      "status_code": 20100,
      "status_message": "Task Created.",
      "time": "0.0041 sec.",
      "cost": 0.0006,
      "result_count": 0,
      "path": [
        "v3",
        "serp",
        "google",
        "search_by_image",
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

- Async task-based endpoint (no live mode). Returns a task_id — use postback_url to receive results or poll tasks_ready.

## Alternatives

- `dataforseo_serp_google_dataset_search`
- `dataforseo_serp_google_finance_ticker_search`
- `dataforseo_app_google_searches`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
