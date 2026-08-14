---
name: dataforseo_kw_dataforseo_trends_demography
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_kw_dataforseo_trends_demography`

Get demographic breakdown of search queries — age and gender distribution of searchers.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `trends` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_kw_dataforseo_trends_demography",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `location_code` | integer | no |  | search engine location code |
| `tag` | string | no |  | user-defined task identifier |
| `time_range` | string | no |  | preset time ranges |
| `type` | string | no |  | type of element |
| `keywords` | string[] | yes |  | List of keywords (up to 1000) |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `date_from` | string | no |  | Start date (YYYY-MM-DD) |
| `date_to` | string | no |  | End date (YYYY-MM-DD) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "location_code": {
      "type": "integer",
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
    "type": {
      "type": "string",
      "description": "type of element"
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
    "date_from": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD)"
    },
    "date_to": {
      "type": "string",
      "description": "End date (YYYY-MM-DD)"
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
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].keywords[]` | array<string> |  |
| `tasks[].result[].type` | string |  |
| `tasks[].result[].location_code` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "1.1455 sec.",
  "cost": 0.0024,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111846-1544-0574-0000-d8091ba19d67",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "1.1395 sec.",
      "cost": 0.0024,
      "result_count": 1,
      "path": [
        "v3",
        "keywords_data",
        "dataforseo_trends",
        "demography",
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

- Use for audience intelligence — understand who searches for specific keywords by age/gender.

- Demographic breakdown of search interest by age and gender — critical for audience targeting.

## Alternatives

- `dataforseo_content_phrase_trends`
- `dataforseo_kw_dataforseo_trends_explore`
- `dataforseo_kw_dataforseo_trends_merged_data`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
