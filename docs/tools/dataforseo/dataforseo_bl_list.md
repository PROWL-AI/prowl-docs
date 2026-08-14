---
name: dataforseo_bl_list
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_list`

Get individual backlinks pointing to a target — with anchor text, dofollow status, page/domain rank.

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
  "tool_name": "dataforseo_bl_list",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `backlinks_status_type` | string | no |  | set what backlinks to return and count |
| `custom_mode` | string | no |  | detailed results grouping type |
| `exclude_internal_backlinks` | boolean | no |  | indicates if internal backlinks from subdomains to the target will be excluded from the results |
| `field` | string | no |  | response field |
| `include_indirect_links` | boolean | no |  | indicates if indirect links to the target will be included in the results |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values |
| `search_after_token` | string | no |  | token for subsequent requests |
| `tag` | string | no |  | user-defined task identifier |
| `value` | integer | no |  | number of backlinks to return per field |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `order_by` | string[] | no |  | Sorting rules over the returned rows (e.g. ['rank,desc'] or ['backlinks,desc']) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `include_subdomains` | boolean | no |  |  |
| `mode` | enum(as_is, one_per_domain, one_per_anchor) | no |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "backlinks_status_type": {
      "type": "string",
      "description": "set what backlinks to return and count"
    },
    "custom_mode": {
      "type": "string",
      "description": "detailed results grouping type"
    },
    "exclude_internal_backlinks": {
      "type": "boolean",
      "description": "indicates if internal backlinks from subdomains to the target will be excluded from the results"
    },
    "field": {
      "type": "string",
      "description": "response field"
    },
    "include_indirect_links": {
      "type": "boolean",
      "description": "indicates if indirect links to the target will be included in the results"
    },
    "rank_scale": {
      "type": "string",
      "description": "defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values"
    },
    "search_after_token": {
      "type": "string",
      "description": "token for subsequent requests"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "value": {
      "type": "integer",
      "description": "number of backlinks to return per field"
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
    "order_by": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Sorting rules over the returned rows (e.g. ['rank,desc'] or ['backlinks,desc'])"
    },
    "filters": {
      "type": "array",
      "description": "DataForSEO filter conditions array"
    },
    "include_subdomains": {
      "type": "boolean"
    },
    "mode": {
      "type": "string",
      "enum": [
        "as_is",
        "one_per_domain",
        "one_per_anchor"
      ]
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
| `tasks[].result[].mode` | null |  |
| `tasks[].result[].custom_mode` | null |  |
| `tasks[].result[].total_count` | integer |  |
| `tasks[].result[].items_count` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0344 sec.",
  "cost": 0.0276,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0269-0000-5b77434202ac",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0286 sec.",
      "cost": 0.0276,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "backlinks",
        "live"
      ],
      "data": {
        "api": "b
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

- Individual backlinks pointing to a target. Returns each backlink with: source URL, anchor text, dofollow status, page rank, domain rank, first_seen/last_seen dates, link type.
- Input: target, optional limit (default 100), mode (as_is/one_per_domain/one_per_anchor), filters, order_by (e.g. ['rank,desc']).
- Response: tasks[].result[] contains individual backlink objects.

## Alternatives

- `majestic_get_back_link_data`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
