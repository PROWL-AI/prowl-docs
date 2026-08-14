---
name: dataforseo_labs_serp_competitors
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_serp_competitors`

Find domains that compete for the specified keywords in SERPs — SERP competitors with traffic estimates.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `competitors`, `dataforseo`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_serp_competitors",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `include_subdomains` | boolean | no |  | indicates if the subdomains will be included in the search |
| `item_types` | any[] | no |  | search results type |
| `language_code` | string | no |  | unique language identifier |
| `location_code` | integer | no |  | unique location identifier |
| `order_by` | any[] | no |  | results sorting rules |
| `tag` | string | no |  | user-defined task identifier |
| `keywords` | string[] | yes |  | List of keywords (up to 1000) |
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
    "include_subdomains": {
      "type": "boolean",
      "description": "indicates if the subdomains will be included in the search"
    },
    "item_types": {
      "type": "array",
      "description": "search results type"
    },
    "language_code": {
      "type": "string",
      "description": "unique language identifier"
    },
    "location_code": {
      "type": "integer",
      "description": "unique location identifier"
    },
    "order_by": {
      "type": "array",
      "description": "results sorting rules"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
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
| `tasks[].data.se_type` | string |  |
| `tasks[].data.keywords[]` | array<string> |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].se_type` | string |  |
| `tasks[].result[].seed_keywords[]` | array<string> |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0787 sec.",
  "cost": 0.02004,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0383-0000-5a0988c33668",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0375 sec.",
      "cost": 0.02004,
      "result_count": 1,
      "path": [
        "v3",
        "dataforseo_labs",
        "google",
        "serp_competitors",
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

- `dataforseo_serp_bing_organic`
- `dataforseo_serp_google_ai_mode`
- `dataforseo_serp_google_autocomplete`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
