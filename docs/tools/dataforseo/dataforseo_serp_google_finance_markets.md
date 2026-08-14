---
name: dataforseo_serp_google_finance_markets
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_google_finance_markets`

Get Google Finance market data — indices, currencies, crypto, and trending tickers (no keyword needed).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `finance`, `google`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_google_finance_markets",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `device` | enum(desktop) | no |  | device type |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `market_type` | string | no |  | type of google finance market |
| `os` | enum(windows) | no |  | device operating system |
| `tag` | string | no |  | user-defined task identifier |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "device": {
      "type": "string",
      "description": "device type",
      "enum": [
        "desktop"
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
    "market_type": {
      "type": "string",
      "description": "type of google finance market"
    },
    "os": {
      "type": "string",
      "description": "device operating system",
      "enum": [
        "windows"
      ]
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
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
  "required": []
}
```

## Example request

```json
{}
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
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].data.device` | string |  |
| `tasks[].data.os` | string |  |
| `tasks[].result[]` | array<object> |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "5.0411 sec.",
  "cost": 0.002,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08102040-1544-0139-0000-79acceca75d1",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "4.8915 sec.",
      "cost": 0.002,
      "result_count": 1,
      "path": [
        "v3",
        "serp",
        "google",
        "finance_markets",
        "live",
        "advanced"
     
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

- Market overview data including indices, sectors, and market movers for macroeconomic context.

## Alternatives

- `dataforseo_serp_google_finance_explore`
- `dataforseo_serp_google_finance_quote`
- `dataforseo_serp_google_finance_ticker_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
