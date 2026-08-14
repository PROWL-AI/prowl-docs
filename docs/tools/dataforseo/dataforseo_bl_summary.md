---
name: dataforseo_bl_summary
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_summary`

Get backlink profile summary — total backlinks, referring domains, rank, spam score, and more.

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
  "tool_name": "dataforseo_bl_summary",
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
| `exclude_internal_backlinks` | boolean | no |  | indicates if internal backlinks from subdomains to the target will be excluded from the results |
| `include_indirect_links` | boolean | no |  | indicates if indirect links to the target will be included in the results |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank, domain_from_rank, and page_from_rank values |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `include_subdomains` | boolean | no |  | Include subdomains in results |
| `internal_list_limit` | integer | no |  |  |

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
      "description": "indicates if internal backlinks from subdomains to the target will be excluded from the results"
    },
    "include_indirect_links": {
      "type": "boolean",
      "description": "indicates if indirect links to the target will be included in the results"
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
    "include_subdomains": {
      "type": "boolean",
      "description": "Include subdomains in results"
    },
    "internal_list_limit": {
      "type": "integer"
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
| `tasks[].result[].first_seen` | string |  |
| `tasks[].result[].lost_date` | null |  |
| `tasks[].result[].rank` | integer |  |
| `tasks[].result[].backlinks` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0137 sec.",
  "cost": 0.024036,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0265-0000-1c8ce8c3a955",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0080 sec.",
      "cost": 0.024036,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "summary",
        "live"
      ],
      "data": {
        "api": 
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

- First tool to use for any backlink analysis — gives a complete overview of the link profile.

- Primary backlink overview tool — run first for any domain. Returns: total backlinks, referring domains/IPs/subnets, domain rank (0-1000), spam score (0-100), dofollow/nofollow ratio, broken backlinks, referring_links_tld distribution, referring_links_types (anchor/redirect/image/form/frame), and referring_links_attributes (nofollow/ugc/sponsored).
- Input: target (domain/URL), optional include_subdomains (default true).
- Response: tasks[].result[] contains backlink_stats object with all metrics.

## Alternatives

- `dataforseo_bl_bulk_backlinks`
- `dataforseo_bl_bulk_ranks`
- `majestic_get_index_item_info`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
