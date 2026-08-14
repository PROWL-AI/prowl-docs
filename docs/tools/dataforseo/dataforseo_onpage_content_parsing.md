---
name: dataforseo_onpage_content_parsing
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_onpage_content_parsing`

Parse page content in real time — extract headings, text, links, and structured content from any URL.

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
  "tool_name": "dataforseo_onpage_content_parsing",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `accept_language` | string | no |  | language header for accessing the website |
| `browser_preset` | string | no |  | preset for browser screen parameters |
| `browser_screen_height` | integer | no |  | browser screen height |
| `browser_screen_scale_factor` | number | no |  | browser screen scale factor |
| `browser_screen_width` | integer | no |  | browser screen width |
| `custom_user_agent` | string | no |  | custom user agent |
| `disable_cookie_popup` | boolean | no |  | disable the cookie popup . optional field |
| `enable_browser_rendering` | boolean | no |  | emulate browser rendering to measure Core Web Vitals |
| `enable_xhr` | boolean | no |  | enable XMLHttpRequest on a page |
| `ip_pool_for_scan` | enum(us, de) | no |  | proxy pool |
| `markdown_view` | boolean | no |  | return page content as markdown |
| `store_raw_html` | boolean | no |  | store HTML of a crawled page |
| `switch_pool` | boolean | no |  | switch proxy pool |
| `url` | string | yes |  | URL to parse |
| `enable_javascript` | boolean | no |  |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "accept_language": {
      "type": "string",
      "description": "language header for accessing the website"
    },
    "browser_preset": {
      "type": "string",
      "description": "preset for browser screen parameters"
    },
    "browser_screen_height": {
      "type": "integer",
      "description": "browser screen height"
    },
    "browser_screen_scale_factor": {
      "type": "number",
      "description": "browser screen scale factor"
    },
    "browser_screen_width": {
      "type": "integer",
      "description": "browser screen width"
    },
    "custom_user_agent": {
      "type": "string",
      "description": "custom user agent"
    },
    "disable_cookie_popup": {
      "type": "boolean",
      "description": "disable the cookie popup . optional field"
    },
    "enable_browser_rendering": {
      "type": "boolean",
      "description": "emulate browser rendering to measure Core Web Vitals"
    },
    "enable_xhr": {
      "type": "boolean",
      "description": "enable XMLHttpRequest on a page"
    },
    "ip_pool_for_scan": {
      "type": "string",
      "description": "proxy pool",
      "enum": [
        "us",
        "de"
      ]
    },
    "markdown_view": {
      "type": "boolean",
      "description": "return page content as markdown"
    },
    "store_raw_html": {
      "type": "boolean",
      "description": "store HTML of a crawled page"
    },
    "switch_pool": {
      "type": "boolean",
      "description": "switch proxy pool"
    },
    "url": {
      "type": "string",
      "description": "URL to parse"
    },
    "enable_javascript": {
      "type": "boolean"
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
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].crawl_progress` | string |  |
| `tasks[].result[].crawl_status` | string |  |
| `tasks[].result[].items_count` | integer |  |
| `tasks[].result[].items` | null |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "2.0603 sec.",
  "cost": 0.00015,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0495-0000-e4b418e938f6",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "2.0529 sec.",
      "cost": 0.00015,
      "result_count": 1,
      "path": [
        "v3",
        "on_page",
        "content_parsing",
        "live"
      ],
      "data": {
        "ap
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

## Alternatives

- `dataforseo_ai_llm_mentions_top_pages`
- `dataforseo_labs_page_intersection`
- `dataforseo_labs_relevant_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
