---
name: dataforseo_ai_llm_mentions_aggregated
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_ai_llm_mentions_aggregated`

Get aggregated LLM mention metrics — total mentions, sentiment, and trends for a domain/keyword in AI search.

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
  "tool_name": "dataforseo_ai_llm_mentions_aggregated",
  "params": {
    "target": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | Keyword or domain to track |
| `platform` | enum(google, chat_gpt) | no |  | AI platform |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "Keyword or domain to track"
    },
    "platform": {
      "type": "string",
      "description": "AI platform",
      "enum": [
        "google",
        "chat_gpt"
      ]
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
| `tasks[].data.target[]` | array<object> |  |
| `tasks[].data.target[].domain` | string |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].total` | object |  |
| `tasks[].result[].total.location[]` | array<object> |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "2.1809 sec.",
  "cost": 0.101,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0635-0000-1a850a98e9ed",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "2.1651 sec.",
      "cost": 0.101,
      "result_count": 1,
      "path": [
        "v3",
        "ai_optimization",
        "llm_mentions",
        "aggregated_metrics",
        "live"
     
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

- Use for AI SEO dashboards — get a high-level view of brand visibility across AI search.

- Aggregated LLM mention metrics over time. Returns time-series data of mention counts, sentiment averages across platforms.
- Input: target, optional platform, location_name, language_name.
- Use for AI visibility trend analysis — track whether AI mentions are growing or declining.

## Alternatives

- `dataforseo_ai_llm_mentions`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
