---
name: dataforseo_onpage_lighthouse
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_onpage_lighthouse`

Run Google Lighthouse audit — performance, accessibility, SEO, and best practices scores.

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
  "tool_name": "dataforseo_onpage_lighthouse",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `audits` | any[] | no |  | Lighthouse audits |
| `language_code` | string | no |  | lighthouse language code |
| `tag` | string | no |  | user-defined task identifier |
| `version` | string | no |  | lighthouse version |
| `url` | string | yes |  | URL to audit |
| `categories` | string[] | no |  | Audit categories |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `for_mobile` | boolean | no |  | Run mobile audit (default desktop) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "audits": {
      "type": "array",
      "description": "Lighthouse audits"
    },
    "language_code": {
      "type": "string",
      "description": "lighthouse language code"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "version": {
      "type": "string",
      "description": "lighthouse version"
    },
    "url": {
      "type": "string",
      "description": "URL to audit"
    },
    "categories": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "performance",
          "accessibility",
          "best_practices",
          "seo"
        ]
      },
      "description": "Audit categories"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "for_mobile": {
      "type": "boolean",
      "description": "Run mobile audit (default desktop)"
    }
  },
  "required": [
    "url"
  ]
}
```

## Example request

```json
{
  "url": "https://example.com"
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
| `tasks[].data.url` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].lighthouseVersion` | string |  |
| `tasks[].result[].requestedUrl` | string |  |
| `tasks[].result[].mainDocumentUrl` | string |  |
| `tasks[].result[].finalDisplayedUrl` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "22.8610 sec.",
  "cost": 0.005,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0324-0000-95e7927de767",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "22.8079 sec.",
      "cost": 0.005,
      "result_count": 1,
      "path": [
        "v3",
        "on_page",
        "lighthouse",
        "live",
        "json"
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

- Use for comprehensive site quality audits — returns Lighthouse scores and detailed audit results.

## Alternatives

- `dataforseo_ai_llm_mentions_top_pages`
- `dataforseo_labs_page_intersection`
- `dataforseo_labs_relevant_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
