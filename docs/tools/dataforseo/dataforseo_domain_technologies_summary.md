---
name: dataforseo_domain_technologies_summary
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_domain_technologies_summary`

Get adoption statistics for technologies — how many domains use specific tech across countries/languages.

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
  "tool_name": "dataforseo_domain_technologies_summary",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `categories` | any[] | no |  | ids of the target technology categories |
| `filters` | any[] | no |  | array of results filtering parameters |
| `groups` | any[] | no |  | ids of the target technology groups |
| `internal_list_limit` | integer | no |  | maximum number of elements within internal arrays |
| `mode` | string | no |  | search mode |
| `tag` | string | no |  | user-defined task identifier |
| `technology_paths` | any[] | no |  | target technology paths |
| `technologies` | string[] | no |  | Technology names (e.g. 'WordPress', 'React') |
| `keywords` | string[] | no |  | List of keywords (up to 1000) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "categories": {
      "type": "array",
      "description": "ids of the target technology categories"
    },
    "filters": {
      "type": "array",
      "description": "array of results filtering parameters"
    },
    "groups": {
      "type": "array",
      "description": "ids of the target technology groups"
    },
    "internal_list_limit": {
      "type": "integer",
      "description": "maximum number of elements within internal arrays"
    },
    "mode": {
      "type": "string",
      "description": "search mode"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "technology_paths": {
      "type": "array",
      "description": "target technology paths"
    },
    "technologies": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Technology names (e.g. 'WordPress', 'React')"
    },
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of keywords (up to 1000)"
    }
  },
  "required": []
}
```

## Example request

```json
{}
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
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].countries` | object |  |
| `tasks[].result[].countries.DE` | integer |  |
| `tasks[].result[].countries.US` | integer |  |
| `tasks[].result[].countries.IN` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "1.2967 sec.",
  "cost": 0.0132,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0492-0000-8f4f02747829",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "1.2378 sec.",
      "cost": 0.0132,
      "result_count": 1,
      "path": [
        "v3",
        "domain_analytics",
        "technologies",
        "technologies_summary",
        "live"

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

- `dataforseo_ai_llm_mentions_top_domains`
- `dataforseo_domain_domains_by_technology`
- `dataforseo_domain_technologies`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
