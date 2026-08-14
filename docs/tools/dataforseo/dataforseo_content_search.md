---
name: dataforseo_content_search
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_content_search`

Search content citations across the web — find where a keyword/brand is mentioned with sentiment data.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `search` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_content_search",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keyword_fields` | string | no |  | target keyword fields and target keywords |
| `offset_token` | string | no |  | offset token for subsequent requests |
| `page_type` | any[] | no |  | target page types |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the domain_rank, and url_rank values |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Search keyword or query |
| `search_mode` | enum(as_is, word) | no |  |  |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `order_by` | string[] | no |  | Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc']) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keyword_fields": {
      "type": "string",
      "description": "target keyword fields and target keywords"
    },
    "offset_token": {
      "type": "string",
      "description": "offset token for subsequent requests"
    },
    "page_type": {
      "type": "array",
      "description": "target page types"
    },
    "rank_scale": {
      "type": "string",
      "description": "defines the scale used for calculating and displaying the domain_rank, and url_rank values"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keyword": {
      "type": "string",
      "description": "Search keyword or query"
    },
    "search_mode": {
      "type": "string",
      "enum": [
        "as_is",
        "word"
      ]
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
| `tasks[].result[].offset_token` | string |  |
| `tasks[].result[].total_count` | integer |  |
| `tasks[].result[].items_count` | integer |  |
| `tasks[].result[].items[]` | array<object> |  |
| `tasks[].result[].items[].type` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "18.1329 sec.",
  "cost": 0.0276,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0463-0000-e70b264be290",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "18.1057 sec.",
      "cost": 0.0276,
      "result_count": 1,
      "path": [
        "v3",
        "content_analysis",
        "search",
        "live"
      ],
      "data": {
        "ap
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

- Use for brand monitoring — find all web mentions of a brand/keyword with sentiment and context.

## Alternatives

- `dataforseo_app_apple_searches`
- `dataforseo_app_google_searches`
- `dataforseo_serp_google_dataset_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
