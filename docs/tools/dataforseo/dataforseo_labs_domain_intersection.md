---
name: dataforseo_labs_domain_intersection
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_domain_intersection`

Find keywords where two domains both rank — discover shared and unique keyword opportunities.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `domain` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_domain_intersection",
  "params": {
    "target1": "example",
    "target2": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `include_clickstream_data` | boolean | no |  | include or exclude data from clickstream-based metrics in the result |
| `include_serp_info` | boolean | no |  | include data from SERP for each keyword |
| `intersections` | boolean | no |  | domain intersections in SERP. optional field |
| `item_types` | any[] | no |  | search results type |
| `language_code` | string | no |  | language code |
| `location_code` | integer | no |  | location code |
| `order_by` | any[] | no |  | results sorting rules |
| `tag` | string | no |  | user-defined task identifier |
| `target_1` | string | no |  | domain |
| `target_2` | string | no |  | domain |
| `target1` | string | yes |  | First domain |
| `target2` | string | yes |  | Second domain |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "include_clickstream_data": {
      "type": "boolean",
      "description": "include or exclude data from clickstream-based metrics in the result"
    },
    "include_serp_info": {
      "type": "boolean",
      "description": "include data from SERP for each keyword"
    },
    "intersections": {
      "type": "boolean",
      "description": "domain intersections in SERP. optional field"
    },
    "item_types": {
      "type": "array",
      "description": "search results type"
    },
    "language_code": {
      "type": "string",
      "description": "language code"
    },
    "location_code": {
      "type": "integer",
      "description": "location code"
    },
    "order_by": {
      "type": "array",
      "description": "results sorting rules"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "target_1": {
      "type": "string",
      "description": "domain"
    },
    "target_2": {
      "type": "string",
      "description": "domain"
    },
    "target1": {
      "type": "string",
      "description": "First domain"
    },
    "target2": {
      "type": "string",
      "description": "Second domain"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
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
    }
  },
  "required": [
    "target1",
    "target2"
  ]
}
```

## Example request

```json
{
  "target1": "example",
  "target2": "example"
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
| `tasks[].data.se_type` | string |  |
| `tasks[].data.target1` | string |  |
| `tasks[].data.target2` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].se_type` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "8.8260 sec.",
  "cost": 0.024,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0389-0000-e84955634424",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "8.7853 sec.",
      "cost": 0.024,
      "result_count": 1,
      "path": [
        "v3",
        "dataforseo_labs",
        "google",
        "domain_intersection",
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

- `spyfu_competing_seo_keywords`
- `dataforseo_labs_page_intersection`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
