---
name: dataforseo_bl_page_intersection
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_page_intersection`

Find domains linking to multiple pages — page-level link gap analysis.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `onpage` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_bl_page_intersection",
  "params": {
    "pages": {}
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `pages` | object | yes |  | Dict mapping page URLs, e.g. {'1': 'url1', '2': 'url2'} |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `order_by` | string[] | no |  | Sorting rules over the returned rows (e.g. ['rank,desc'] or ['backlinks,desc']) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |
| `exclude_targets` | string[] | no |  | Domains to exclude |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "pages": {
      "type": "object",
      "description": "Dict mapping page URLs, e.g. {'1': 'url1', '2': 'url2'}"
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
    "exclude_targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Domains to exclude"
    }
  },
  "required": [
    "pages"
  ]
}
```

## Example request

```json
{
  "pages": {}
}
```

## Output

_No output schema or active profile response_format._

> Profile capture status: **error** — DataForSEOError: DataForSEO task errors: 40501: Invalid Field: 'targets'.

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

- Page-level link gap — finds domains linking to specific competitor pages but not to yours.
- Input: pages (dict mapping, e.g. {'1': 'competitor-page.com/blog', '2': 'your-page.com/blog'}), optional exclude_targets, limit, filters.
- More precise than domain_intersection — targets specific content gaps.

## Alternatives

- `dataforseo_bl_domain_intersection`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
