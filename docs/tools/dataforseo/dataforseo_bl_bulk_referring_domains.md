---
name: dataforseo_bl_bulk_referring_domains
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_bulk_referring_domains`

Get referring domain counts for up to 1000 targets in one request.

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
  "tool_name": "dataforseo_bl_bulk_referring_domains",
  "params": {
    "targets": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `targets` | string[] | yes |  | List of target domains/URLs (up to 1000) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of target domains/URLs (up to 1000)"
    }
  },
  "required": [
    "targets"
  ]
}
```

## Example request

```json
{
  "targets": []
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
| `tasks[].data.targets[]` | array<string> |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].items_count` | integer |  |
| `tasks[].result[].items[]` | array<object> |  |
| `tasks[].result[].items[].target` | string |  |
| `tasks[].result[].items[].referring_domains` | integer |  |
| `tasks[].result[].items[].referring_domains_nofollow` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.2365 sec.",
  "cost": 0.024072,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111839-1544-0351-0000-d3e5800aaa27",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "0.0083 sec.",
      "cost": 0.024072,
      "result_count": 1,
      "path": [
        "v3",
        "backlinks",
        "bulk_referring_domains",
        "live"
      ],
      "data": {

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

- Referring domain counts for up to 1000 targets in one request.
- Input: targets (list of URLs/domains).
- Quick authority comparison across many domains.

## Alternatives

- `dataforseo_ai_llm_mentions_top_domains`
- `dataforseo_domain_domains_by_technology`
- `dataforseo_domain_technologies`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
