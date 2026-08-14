---
name: dataforseo_serp_google_jobs
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_jobs`

Create a Google Jobs SERP task (async) — job listings from Google for Jobs.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | 150.0 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_google_jobs",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `employment_type` | any[] | no |  | employment contract type |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `location_radius` | string | no |  | location search radius |
| `postback_data` | string | no |  | postback_url datatype |
| `priority` | integer | no |  | task priority |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `depth` | integer | no |  | Number of results to return (max 200) |
| `pingback_url` | string | no |  | Notification URL when task is ready |
| `postback_url` | string | no |  | URL to receive results when ready |
| `tag` | string | no |  | User-defined task tag |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "employment_type": {
      "type": "array",
      "description": "employment contract type"
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "location_radius": {
      "type": "string",
      "description": "location search radius"
    },
    "postback_data": {
      "type": "string",
      "description": "postback_url datatype"
    },
    "priority": {
      "type": "integer",
      "description": "task priority"
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
      "description": "Number of results to return (max 200)",
      "minimum": 1,
      "maximum": 200
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
  "time": "0.0489 sec.",
  "cost": 0.0006,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0447-0000-34bd9140caeb",
      "status_code": 20100,
      "status_message": "Task Created.",
      "time": "0.0039 sec.",
      "cost": 0.0006,
      "result_count": 0,
      "path": [
        "v3",
        "serp",
        "google",
        "jobs",
        "task_post"
      ],
      "dat
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

- `dataforseo_serp_google_ai_mode`
- `dataforseo_serp_google_autocomplete`
- `dataforseo_serp_google_dataset_info`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
