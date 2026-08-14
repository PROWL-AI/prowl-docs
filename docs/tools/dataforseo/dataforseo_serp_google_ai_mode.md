---
name: dataforseo_serp_google_ai_mode
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_ai_mode`

Get Google AI Mode SERP results — AI-generated answers from Google's AI Mode feature.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_google_ai_mode",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `browser_screen_height` | integer | no |  | browser screen height |
| `browser_screen_resolution_ratio` | integer | no |  | browser screen resolution ratio |
| `browser_screen_width` | integer | no |  | browser screen width |
| `calculate_rectangles` | boolean | no |  | calculate pixel rankings for SERP elements in advanced results |
| `device` | enum(desktop, mobile) | no |  | device type |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `os` | string | no |  | device operating system |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Search keyword or query |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "browser_screen_height": {
      "type": "integer",
      "description": "browser screen height"
    },
    "browser_screen_resolution_ratio": {
      "type": "integer",
      "description": "browser screen resolution ratio"
    },
    "browser_screen_width": {
      "type": "integer",
      "description": "browser screen width"
    },
    "calculate_rectangles": {
      "type": "boolean",
      "description": "calculate pixel rankings for SERP elements in advanced results"
    },
    "device": {
      "type": "string",
      "description": "device type",
      "enum": [
        "desktop",
        "mobile"
      ]
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "location_coordinate": {
      "type": "string",
      "description": "GPS coordinates of a location"
    },
    "os": {
      "type": "string",
      "description": "device operating system"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keyword": {
      "type": "string",
      "description": "Search keyword or query"
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
    "keyword"
  ]
}
```

## Example request

```json
{
  "keyword": "example query"
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
| `tasks[].data.se` | string |  |
| `tasks[].data.se_type` | string |  |
| `tasks[].data.keyword` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].data.device` | string |  |
| `tasks[].data.os` | string |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "4.2999 sec.",
  "cost": 0.004,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0139-0000-e0b09a3adeac",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "4.2152 sec.",
      "cost": 0.004,
      "result_count": 1,
      "path": [
        "v3",
        "serp",
        "google",
        "ai_mode",
        "live",
        "advanced"
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

- Use to analyze Google AI Overviews and AI-generated answers for SEO optimization.

## Alternatives

- `google_ai_mode`
- `google_ai_overview`
- `dataforseo_serp_ai_summary`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
