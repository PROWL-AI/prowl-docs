---
name: dataforseo_bl_domain_intersection
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_bl_domain_intersection`

Find domains linking to your competitors but not to you — link gap analysis.

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
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_bl_domain_intersection",
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
| `exclude_targets` | string[] | no |  | Domains to exclude |
| `limit` | integer | no |  | Max number of results |
| `offset` | integer | no |  | Offset for pagination |
| `order_by` | string[] | no |  | Sorting rules over the returned rows (e.g. ['rank,desc'] or ['backlinks,desc']) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

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
    },
    "exclude_targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Domains to exclude"
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

_No output schema or active profile response_format._

> Profile capture status: **error** — DataForSEOError: DataForSEO task errors: 50000: Internal Error.

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- Essential for link building — finds sites that link to competitors but not to you.

- Link gap analysis — finds domains linking to competitors but not to target. The primary backlink gap tool.
- Input: targets (list of competitor domains), optional exclude_targets (your domain), limit, filters, order_by.
- Response: referring domains with which targets they link to. Use to build outreach lists.

## Alternatives

- `dataforseo_bl_page_intersection`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
