---
name: dataforseo_biz_tripadvisor_search
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_biz_tripadvisor_search`

Search Tripadvisor business profiles — find hotels, restaurants, and attractions.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `dataforseo`, `search` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_biz_tripadvisor_search",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `depth` | integer | no |  | parsing depth |
| `location_code` | integer | no |  | search engine location code |
| `pingback_url` | string | no |  | notification URL of a completed task |
| `postback_url` | string | no |  | URL for sending task results |
| `priority` | integer | no |  | task priority |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Business name or keyword |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "depth": {
      "type": "integer",
      "description": "parsing depth"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "pingback_url": {
      "type": "string",
      "description": "notification URL of a completed task"
    },
    "postback_url": {
      "type": "string",
      "description": "URL for sending task results"
    },
    "priority": {
      "type": "integer",
      "description": "task priority"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keyword": {
      "type": "string",
      "description": "Business name or keyword"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
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
| `tasks[].data.se_type` | string |  |
| `tasks[].data.se` | string |  |
| `tasks[].data.device` | string |  |
| `tasks[].data.os` | string |  |
| `tasks[].result` | null |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.1370 sec.",
  "cost": 0.00075,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0393-0000-6f7262c3df8c",
      "status_code": 20100,
      "status_message": "Task Created.",
      "time": "0.0062 sec.",
      "cost": 0.00075,
      "result_count": 0,
      "path": [
        "v3",
        "business_data",
        "tripadvisor",
        "search",
        "task_post"
 
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

- `google_ads_transparency_advertiser_search`
- `meta_ad_library_page_search`
- `tiktok_ads_library_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
