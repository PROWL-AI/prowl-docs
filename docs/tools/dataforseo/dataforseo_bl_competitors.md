---
name: dataforseo_bl_competitors
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_competitors`

Find backlink competitors — domains sharing the most backlink overlap with the target.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `competitors`, `dataforseo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_bl_competitors",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `exclude_internal_backlinks` | boolean | no |  | indicates if internal backlinks from subdomains to the target will be excluded from the results |
| `exclude_large_domains` | boolean | no |  | indicates whether large domain will appear in results |
| `main_domain` | boolean | no |  | indicates if only main domain of the target will be included in the search |
| `order_by` | string[] | no |  | Sorting rules over the returned rows (e.g. ['rank,desc'] or ['intersections,desc']); live-verified 2026-08-12 |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "exclude_internal_backlinks": {
      "type": "boolean",
      "description": "indicates if internal backlinks from subdomains to the target will be excluded from the results"
    },
    "exclude_large_domains": {
      "type": "boolean",
      "description": "indicates whether large domain will appear in results"
    },
    "main_domain": {
      "type": "boolean",
      "description": "indicates if only main domain of the target will be included in the search"
    },
    "order_by": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Sorting rules over the returned rows (e.g. ['rank,desc'] or ['intersections,desc']); live-verified 2026-08-12"
    },
    "rank_scale": {
      "type": "string",
      "description": "defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
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
| `tasks[].result[].total_count` | integer |  |
| `tasks[].result[].items_count` | integer |  |
| `tasks[].result[].items[]` | array<object> |  |
| `tasks[].result[].items[].type` | string |  |
| `tasks[].result[].items[].target` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "11.0406 sec.",
  "cost": 0.0276,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0461-0000-3015e7cc8f81",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "11.0300 sec.",
      "cost": 0.0276,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "competitors",
        "live"
      ],
      "data": {
        "api"
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

- Domains sharing the most backlink overlap with target. Returns competitor domains ranked by intersection score.
- Input: target, optional limit, filters.
- Run to discover which domains compete for the same link sources — actionable for link-building strategy.

## Alternatives

- `dataforseo_labs_competitors_domain`
- `dataforseo_labs_serp_competitors`
- `spyfu_get_combined_competitors`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
