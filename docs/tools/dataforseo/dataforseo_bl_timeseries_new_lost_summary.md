---
name: dataforseo_bl_timeseries_new_lost_summary
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_timeseries_new_lost_summary`

Get new/lost backlink trends over time — daily new and lost backlink counts.

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
  "tool_name": "dataforseo_bl_timeseries_new_lost_summary",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `group_range` | enum(day, week, month, year) | no |  | time range which will be used to group the results |
| `include_subdomains` | boolean | no |  | indicates if the subdomains of the target will be included in the search |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `date_from` | string | no |  | Start date (YYYY-MM-DD) |
| `date_to` | string | no |  | End date (YYYY-MM-DD) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "group_range": {
      "type": "string",
      "description": "time range which will be used to group the results",
      "enum": [
        "day",
        "week",
        "month",
        "year"
      ]
    },
    "include_subdomains": {
      "type": "boolean",
      "description": "indicates if the subdomains of the target will be included in the search"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "target": {
      "type": "string",
      "description": "Target domain, subdomain, or URL (e.g. 'example.com')"
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
| `tasks[].data.target` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].target` | string |  |
| `tasks[].result[].date_from` | null |  |
| `tasks[].result[].date_to` | null |  |
| `tasks[].result[].group_range` | string |  |
| `tasks[].result[].items_count` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0631 sec.",
  "cost": 0.027312,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0460-0000-e3df9a3b5fd2",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0284 sec.",
      "cost": 0.027312,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "timeseries_new_lost_summary",
        "live"
      ],
      "data
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

- New vs lost backlinks over time. Returns daily: new_backlinks, lost_backlinks, new_referring_domains, lost_referring_domains.
- Input: target, optional date_from/date_to.
- Shows whether a domain is gaining or losing authority momentum.

## Alternatives

- `dataforseo_bl_timeseries_summary`
- `dataforseo_bl_bulk_new_lost_backlinks`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
