---
name: dataforseo_bl_referring_domains
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_referring_domains`

Get referring domains pointing to a target — unique domains linking to you.

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
  "tool_name": "dataforseo_bl_referring_domains",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `backlinks_filters` | any[] | no |  | filter the backlinks of your target |
| `backlinks_status_type` | string | no |  | set what backlinks to return and count |
| `exclude_internal_backlinks` | boolean | no |  | indicates whether the backlinks from subdomains of the target are excluded |
| `include_indirect_links` | boolean | no |  | indicates if indirect links to the target will be included in the results |
| `internal_list_limit` | integer | no |  | maximum number of elements within internal arrays |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `order_by` | string[] | no |  | Sorting rules over the returned rows (e.g. ['rank,desc'] or ['backlinks,desc']) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `include_subdomains` | boolean | no |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "backlinks_filters": {
      "type": "array",
      "description": "filter the backlinks of your target"
    },
    "backlinks_status_type": {
      "type": "string",
      "description": "set what backlinks to return and count"
    },
    "exclude_internal_backlinks": {
      "type": "boolean",
      "description": "indicates whether the backlinks from subdomains of the target are excluded"
    },
    "include_indirect_links": {
      "type": "boolean",
      "description": "indicates if indirect links to the target will be included in the results"
    },
    "internal_list_limit": {
      "type": "integer",
      "description": "maximum number of elements within internal arrays"
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
  "time": "0.0262 sec.",
  "cost": 0.0276,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0273-0000-8c39fa85fb6f",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0182 sec.",
      "cost": 0.0276,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "referring_domains",
        "live"
      ],
      "data": {
        "
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

- Unique referring domains linking to target. Returns each domain with: rank, backlinks count, dofollow count, first_seen, broken links.
- Input: target, optional limit, include_subdomains, filters, order_by (e.g. ['rank,desc'] for highest-authority first).
- Use order_by=['rank,desc'] to find highest-authority referring domains.

## Alternatives

- `majestic_get_ref_domains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
