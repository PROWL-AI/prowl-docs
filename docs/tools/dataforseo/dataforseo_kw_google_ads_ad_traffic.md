---
name: dataforseo_kw_google_ads_ad_traffic
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_kw_google_ads_ad_traffic`

Estimate Google Ads traffic for keywords — predicted clicks, impressions, CPC, and cost at given bid.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `dataforseo`, `google` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_kw_google_ads_ad_traffic",
  "params": {
    "bid": "bid_example",
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `date_from` | string | no |  | starting date of the forecasting time range |
| `date_interval` | enum(next_week, next_month, next_quarter) | no |  | forecasting date interval |
| `date_to` | string | no |  | ending date of the forecasting time range |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `search_partners` | boolean | no |  | include Google search partners |
| `sort_by` | string | no |  | results sorting parameters |
| `tag` | string | no |  | user-defined task identifier |
| `keywords` | string[] | yes |  | List of keywords (up to 1000) |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `bid` | number | yes |  | Max CPC bid in USD (required) |
| `match` | enum(exact, broad, phrase) | no |  | Match type |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "date_from": {
      "type": "string",
      "description": "starting date of the forecasting time range"
    },
    "date_interval": {
      "type": "string",
      "description": "forecasting date interval",
      "enum": [
        "next_week",
        "next_month",
        "next_quarter"
      ]
    },
    "date_to": {
      "type": "string",
      "description": "ending date of the forecasting time range"
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
    "search_partners": {
      "type": "boolean",
      "description": "include Google search partners"
    },
    "sort_by": {
      "type": "string",
      "description": "results sorting parameters"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of keywords (up to 1000)"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "bid": {
      "type": "number",
      "description": "Max CPC bid in USD (required)"
    },
    "match": {
      "type": "string",
      "description": "Match type",
      "enum": [
        "exact",
        "broad",
        "phrase"
      ]
    }
  },
  "required": [
    "keywords",
    "bid"
  ]
}
```

## Example request

```json
{
  "bid": "bid_example",
  "keywords": []
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
| `tasks[].data.keywords[]` | array<string> |  |
| `tasks[].data.location_name` | string |  |
| `tasks[].data.language_name` | string |  |
| `tasks[].data.bid` | integer |  |
| `tasks[].data.match` | string |  |
| `tasks[].result[]` | array<object> |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "2.5124 sec.",
  "cost": 0.09,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111838-1544-0370-0000-9fab8370754c",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "2.4958 sec.",
      "cost": 0.09,
      "result_count": 1,
      "path": [
        "v3",
        "keywords_data",
        "google_ads",
        "ad_traffic_by_keywords",
        "live"
      ]
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

- `dataforseo_kw_google_ads_keywords_for_keywords`
- `dataforseo_kw_google_ads_keywords_for_site`
- `dataforseo_kw_google_ads_search_volume`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
