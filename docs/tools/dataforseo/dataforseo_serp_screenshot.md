---
name: dataforseo_serp_screenshot
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_screenshot`

Capture a screenshot of SERP results — requires a task_id from a prior SERP task_post.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `dataforseo`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_screenshot",
  "params": {
    "task_id": "01234567-89ab-cdef-0123-456789abcdef"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `task_id` | string | yes |  | Task ID (UUID) from a prior SERP task_post |
| `browser_preset` | string | no |  | Browser preset: desktop, tablet, or mobile |
| `browser_screen_width` | integer | no |  | Browser viewport width (240-9999) |
| `browser_screen_height` | integer | no |  | Browser viewport height (240-9999) |
| `browser_screen_scale_factor` | number | no |  | Device scale factor (0.5-3) |
| `page` | integer | no |  | SERP page number to screenshot (default 1) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "task_id": {
      "type": "string",
      "description": "Task ID (UUID) from a prior SERP task_post"
    },
    "browser_preset": {
      "type": "string",
      "description": "Browser preset: desktop, tablet, or mobile"
    },
    "browser_screen_width": {
      "type": "integer",
      "description": "Browser viewport width (240-9999)"
    },
    "browser_screen_height": {
      "type": "integer",
      "description": "Browser viewport height (240-9999)"
    },
    "browser_screen_scale_factor": {
      "type": "number",
      "description": "Device scale factor (0.5-3)"
    },
    "page": {
      "type": "integer",
      "description": "SERP page number to screenshot (default 1)"
    }
  },
  "required": [
    "task_id"
  ]
}
```

## Example request

```json
{
  "task_id": "01234567-89ab-cdef-0123-456789abcdef"
}
```

## Output

Top-level keys: `version`, `status_code`, `status_message`, `time`, `cost`, `tasks_count`, `tasks_error`, `tasks`

| Path | Type | Description |
|------|------|-------------|
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].keyword` | string |  |
| `tasks[].result[].items[]` | array<object> |  |

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- This is a two-step tool: first submit a SERP task_post, then pass the task_id here.

- Capture page screenshots via SERP infrastructure for visual competitive analysis.

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'dataforseo_serp_google_organic', 'extract': '?'}`

## Alternatives

- `dataforseo_serp_ai_summary`
- `dataforseo_serp_bing_organic`
- `dataforseo_serp_google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
