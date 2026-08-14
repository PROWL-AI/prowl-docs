---
name: dataforseo_onpage_links
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_onpage_links`

Get internal and external links found during a crawl.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `dataforseo`, `onpage` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_onpage_links",
  "params": {
    "task_id": "01234567-89ab-cdef-0123-456789abcdef"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `page_from` | string | no |  | relative page URL. optional field |
| `page_to` | string | no |  | relative page URL. optional field |
| `search_after_token` | string | no |  | token for subsequent requests |
| `tag` | string | no |  | user-defined task identifier |
| `task_id` | string | yes |  |  |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `order_by` | string[] | no |  | Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc']) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "page_from": {
      "type": "string",
      "description": "relative page URL. optional field"
    },
    "page_to": {
      "type": "string",
      "description": "relative page URL. optional field"
    },
    "search_after_token": {
      "type": "string",
      "description": "token for subsequent requests"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "task_id": {
      "type": "string"
    },
    "limit": {
      "type": "integer",
      "description": "Max number of results",
      "minimum": 1
    },
    "offset": {
      "type": "integer",
      "description": "Offset for pagination",
      "minimum": 0
    },
    "filters": {
      "type": "array",
      "description": "DataForSEO filter conditions array"
    },
    "order_by": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc'])"
    }
  },
  "required": [
    "task_id"
  ]
}
```

## Example request

```json
{
  "task_id": "01234567-89ab-cdef-0123-456789abcdef"
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
| `cost` | integer |  |
| `tasks_count` | integer |  |
| `tasks_error` | integer |  |
| `tasks[]` | array<object> |  |
| `tasks[].id` | string |  |
| `tasks[].status_code` | integer |  |
| `tasks[].status_message` | string |  |
| `tasks[].time` | string |  |
| `tasks[].cost` | integer |  |
| `tasks[].result_count` | integer |  |
| `tasks[].path[]` | array<string> |  |
| `tasks[].data` | object |  |
| `tasks[].result` | null |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260327",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0501 sec.",
  "cost": 0,
  "tasks_count": 1,
  "tasks_error": 1,
  "tasks": [
    {
      "id": "03282354-1544-0216-0000-ac3a48117456",
      "status_code": 40401,
      "status_message": "Task Not Found.",
      "time": "0.0000 sec.",
      "cost": 0,
      "result_count": 0,
      "path": [
        "v3",
        "on_page",
        "links"
      ],
      "data": {
        "api": "on_page",
        "fu
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

**Chain inputs:** `{'param': 'task_id', 'from_tool': 'dataforseo_onpage_task_post', 'extract': 'tasks[].id'}`

**Chain groups:** `dataforseo_onpage`

## Alternatives

- `dataforseo_ai_llm_mentions_top_pages`
- `dataforseo_labs_page_intersection`
- `dataforseo_labs_relevant_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
