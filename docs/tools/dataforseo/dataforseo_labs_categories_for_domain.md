---
name: dataforseo_labs_categories_for_domain
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_categories_for_domain`

Get Google categories assigned to a domain — understand how Google classifies a website.

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
  "tool_name": "dataforseo_labs_categories_for_domain",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `filters` | any[] | no |  | array of results filtering parameters |
| `historical_serp_mode` | string | no |  | data collection mode |
| `include_clickstream_data` | boolean | no |  | include or exclude data from clickstream-based metrics in the result |
| `include_subcategories` | boolean | no |  | indicates if the subcategories will be included in the search |
| `item_types` | any[] | no |  | display results by item type |
| `language_code` | string | no |  | language code |
| `limit` | integer | no |  | the maximum number of returned categories |
| `location_code` | integer | no |  | location code |
| `offset` | integer | no |  | offset in the results array of returned categories . optional field |
| `order_by` | any[] | no |  | results sorting rules |
| `tag` | string | no |  | user-defined task identifier |
| `target` | string | yes |  | Target domain, subdomain, or URL (e.g. 'example.com') |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "filters": {
      "type": "array",
      "description": "array of results filtering parameters"
    },
    "historical_serp_mode": {
      "type": "string",
      "description": "data collection mode"
    },
    "include_clickstream_data": {
      "type": "boolean",
      "description": "include or exclude data from clickstream-based metrics in the result"
    },
    "include_subcategories": {
      "type": "boolean",
      "description": "indicates if the subcategories will be included in the search"
    },
    "item_types": {
      "type": "array",
      "description": "display results by item type"
    },
    "language_code": {
      "type": "string",
      "description": "language code"
    },
    "limit": {
      "type": "integer",
      "description": "the maximum number of returned categories"
    },
    "location_code": {
      "type": "integer",
      "description": "location code"
    },
    "offset": {
      "type": "integer",
      "description": "offset in the results array of returned categories . optional field"
    },
    "order_by": {
      "type": "array",
      "description": "results sorting rules"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "target": {
      "type": "string",
      "description": "Target domain, subdomain, or URL (e.g. 'example.com')"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
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
| `tasks[].data.se_type` | string |  |
| `tasks[].data.target` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].se_type` | string |  |
| `tasks[].result[].target` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "3.3311 sec.",
  "cost": 0.024,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0402-0000-1f7f9f165c80",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "3.3249 sec.",
      "cost": 0.024,
      "result_count": 1,
      "path": [
        "v3",
        "dataforseo_labs",
        "google",
        "categories_for_domain",
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

- Google content category classification for a domain — reveals how Google perceives topical focus.

## Alternatives

- `dataforseo_ai_llm_mentions_top_domains`
- `dataforseo_domain_domains_by_technology`
- `dataforseo_domain_technologies`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
