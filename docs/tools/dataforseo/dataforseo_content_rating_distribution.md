---
name: dataforseo_content_rating_distribution
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_content_rating_distribution`

Get rating distribution for keyword citations — see how ratings are distributed across mentions.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_content_rating_distribution",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `initial_dataset_filters` | any[] | no |  | initial dataset filtering parameters |
| `internal_list_limit` | integer | no |  | maximum number of elements within internal arrays |
| `keyword_fields` | string | no |  | target keyword fields and target keywords |
| `page_type` | any[] | no |  | target page types |
| `positive_connotation_threshold` | number | no |  | positive connotation threshold |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank values |
| `search_mode` | string | no |  | results grouping type |
| `sentiments_connotation_threshold` | number | no |  | sentiment connotation threshold |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Search keyword or query |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "initial_dataset_filters": {
      "type": "array",
      "description": "initial dataset filtering parameters"
    },
    "internal_list_limit": {
      "type": "integer",
      "description": "maximum number of elements within internal arrays"
    },
    "keyword_fields": {
      "type": "string",
      "description": "target keyword fields and target keywords"
    },
    "page_type": {
      "type": "array",
      "description": "target page types"
    },
    "positive_connotation_threshold": {
      "type": "number",
      "description": "positive connotation threshold"
    },
    "rank_scale": {
      "type": "string",
      "description": "defines the scale used for calculating and displaying the rank values"
    },
    "search_mode": {
      "type": "string",
      "description": "results grouping type"
    },
    "sentiments_connotation_threshold": {
      "type": "number",
      "description": "sentiment connotation threshold"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keyword": {
      "type": "string",
      "description": "Search keyword or query"
    },
    "filters": {
      "type": "array",
      "description": "DataForSEO filter conditions array"
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
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].type` | string |  |
| `tasks[].result[].min` | integer |  |
| `tasks[].result[].max` | number |  |
| `tasks[].result[].metrics` | object |  |
| `tasks[].result[].metrics.type` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.7283 sec.",
  "cost": 0.024,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0466-0000-3db3075c8937",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.7098 sec.",
      "cost": 0.024,
      "result_count": 10,
      "path": [
        "v3",
        "content_analysis",
        "rating_distribution",
        "live"
      ],
      "data": {
 
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

_None listed._

## Provider docs

https://docs.dataforseo.com/v3/
