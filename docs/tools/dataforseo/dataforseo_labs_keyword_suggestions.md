---
name: dataforseo_labs_keyword_suggestions
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_keyword_suggestions`

Get keyword suggestions that include the seed keyword — find long-tail variations.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_keyword_suggestions",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `exact_match` | boolean | no |  | search for the exact phrase |
| `ignore_synonyms` | boolean | no |  | ignore highly similar keywords |
| `include_clickstream_data` | boolean | no |  | include or exclude data from clickstream-based metrics in the result |
| `include_seed_keyword` | boolean | no |  | include data for the seed keyword |
| `include_serp_info` | boolean | no |  | include data from SERP for each keyword |
| `language_code` | string | no |  | language code |
| `location_code` | integer | no |  | location code |
| `offset_token` | string | no |  | offset token for subsequent requests |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `order_by` | string[] | no |  | Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc']) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "exact_match": {
      "type": "boolean",
      "description": "search for the exact phrase"
    },
    "ignore_synonyms": {
      "type": "boolean",
      "description": "ignore highly similar keywords"
    },
    "include_clickstream_data": {
      "type": "boolean",
      "description": "include or exclude data from clickstream-based metrics in the result"
    },
    "include_seed_keyword": {
      "type": "boolean",
      "description": "include data for the seed keyword"
    },
    "include_serp_info": {
      "type": "boolean",
      "description": "include data from SERP for each keyword"
    },
    "language_code": {
      "type": "string",
      "description": "language code"
    },
    "location_code": {
      "type": "integer",
      "description": "location code"
    },
    "offset_token": {
      "type": "string",
      "description": "offset token for subsequent requests"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
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
    "order_by": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc'])"
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
| `tasks[].data.se_type` | string |  |
| `tasks[].data.keyword` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].se_type` | string |  |
| `tasks[].result[].seed_keyword` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.3197 sec.",
  "cost": 0.024,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0399-0000-7e69b213382e",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.3109 sec.",
      "cost": 0.024,
      "result_count": 1,
      "path": [
        "v3",
        "dataforseo_labs",
        "google",
        "keyword_suggestions",
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

- `dataforseo_ai_keyword_volume`
- `dataforseo_labs_amazon_product_keyword_intersections`
- `dataforseo_labs_amazon_related_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
