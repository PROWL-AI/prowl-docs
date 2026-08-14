---
name: dataforseo_domain_whois
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_domain_whois`

Get WHOIS data enriched with backlink stats, rankings, and traffic info for a domain.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `domain`, `whois` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_domain_whois",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `order_by` | string[] | no |  | Sorting rules (e.g. ['keyword_data.keyword_info.search_volume,desc']) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "Target domain, subdomain, or URL (e.g. 'example.com')"
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
    "target"
  ]
}
```

## Example request

```json
{
  "target": "example.com"
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
| `tasks[].data.filters[]` | array<array> |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].total_count` | integer |  |
| `tasks[].result[].items_count` | integer |  |
| `tasks[].result[].offset` | integer |  |
| `tasks[].result[].offset_token` | null |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0876 sec.",
  "cost": 0.1212,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0481-0000-6f5d191cb773",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0633 sec.",
      "cost": 0.1212,
      "result_count": 1,
      "path": [
        "v3",
        "domain_analytics",
        "whois",
        "overview",
        "live"
      ],
      "dat
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

- `dataforseo_labs_domain_whois_overview`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
