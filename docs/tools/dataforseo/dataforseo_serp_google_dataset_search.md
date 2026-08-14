---
name: dataforseo_serp_google_dataset_search
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_dataset_search`

Search Google Dataset Search — find public datasets by keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
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
  "tool_name": "dataforseo_serp_google_dataset_search",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `device` | enum(desktop) | no |  | device type |
| `file_formats` | enum(other, archive, text, image, document, tabular) | no |  | file formats of the dataset |
| `is_free` | enum(true, false) | no |  | indicates whether displayed datasets are free |
| `language_code` | string | no |  | search engine language code |
| `last_updated` | enum(1m, 1y, 3y) | no |  | last time the dataset was updated |
| `os` | string | no |  | device operating system |
| `tag` | string | no |  | user-defined task identifier |
| `topics` | enum(humanities, social_sciences, life_sciences, agriculture, natural_sciences, geo, computer, engineering) | no |  | dataset topics |
| `usage_rights` | enum(commercial, noncommercial) | no |  | usage rights of the dataset |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `depth` | integer | no |  | Number of results to return (max 700) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "device": {
      "type": "string",
      "description": "device type",
      "enum": [
        "desktop"
      ]
    },
    "file_formats": {
      "type": "array",
      "description": "file formats of the dataset",
      "enum": [
        "other",
        "archive",
        "text",
        "image",
        "document",
        "tabular"
      ]
    },
    "is_free": {
      "type": "boolean",
      "description": "indicates whether displayed datasets are free",
      "enum": [
        "true",
        "false"
      ]
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "last_updated": {
      "type": "string",
      "description": "last time the dataset was updated",
      "enum": [
        "1m",
        "1y",
        "3y"
      ]
    },
    "os": {
      "type": "string",
      "description": "device operating system"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "topics": {
      "type": "array",
      "description": "dataset topics",
      "enum": [
        "humanities",
        "social_sciences",
        "life_sciences",
        "agriculture",
        "natural_sciences",
        "geo",
        "computer",
        "engineering"
      ]
    },
    "usage_rights": {
      "type": "string",
      "description": "usage rights of the dataset",
      "enum": [
        "commercial",
        "noncommercial"
      ]
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
      "description": "Number of results to return (max 700)",
      "minimum": 1,
      "maximum": 700
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
  "time": "11.2499 sec.",
  "cost": 0.002,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0139-0000-04f45198d85b",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "11.0003 sec.",
      "cost": 0.002,
      "result_count": 1,
      "path": [
        "v3",
        "serp",
        "google",
        "dataset_search",
        "live",
        "advanced"
    
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

- Search Google Dataset Search for structured public datasets by keyword — useful for market research enrichment.

## Alternatives

- `dataforseo_serp_google_finance_ticker_search`
- `dataforseo_serp_google_search_by_image`
- `dataforseo_app_google_searches`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
