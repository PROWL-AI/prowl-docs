---
name: dataforseo_labs_google_bulk_app_metrics
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_google_bulk_app_metrics`

Retrieve keyword ranking metrics for up to 1000 Google Play app IDs in bulk.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_google_bulk_app_metrics",
  "params": {
    "app_ids": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `app_ids` | any[] | yes |  | Google Play app IDs (up to 1000). E.g. 'org.telegram.messenger' from the Play Store URL. |
| `location_name` | string | no |  | Location name. Required if location_code omitted. Currently US only. |
| `location_code` | integer | no |  | Location code (e.g. 2840 for US). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. Currently English only. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "app_ids": {
      "type": "array",
      "description": "Google Play app IDs (up to 1000). E.g. 'org.telegram.messenger' from the Play Store URL."
    },
    "location_name": {
      "type": "string",
      "description": "Location name. Required if location_code omitted. Currently US only."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840 for US). Required if location_name omitted."
    },
    "language_name": {
      "type": "string",
      "description": "Language name (e.g. 'English'). Required if language_code omitted. Currently English only."
    },
    "language_code": {
      "type": "string",
      "description": "Language code (e.g. 'en'). Required if language_name omitted."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `dataforseo_labs/google/bulk_app_metrics/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "app_ids"
  ]
}
```

## Example request

```json
{
  "app_ids": []
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].se_type` | string |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].total_count` | integer |  |
| `[].items_count` | integer |  |
| `[].items[]` | array<object> |  |
| `[].items[].se_type` | string |  |
| `[].items[].app_id` | string |  |
| `[].items[].metrics` | object |  |
| `[].items[].metrics.google_play_search_organic` | object |  |
| `[].items[].metrics.google_play_search_organic.pos_1` | integer |  |
| `[].items[].metrics.google_play_search_organic.pos_2_3` | integer |  |
| `[].items[].metrics.google_play_search_organic.pos_4_10` | integer |  |
| `[].items[].metrics.google_play_search_organic.pos_11_100` | integer |  |
| `[].items[].metrics.google_play_search_organic.count` | integer |  |
| `[].items[].metrics.google_play_search_organic.search_volume` | integer |  |

### Example response (from profile)

```json
[
  {
    "se_type": "google",
    "location_code": 2840,
    "language_code": "en",
    "total_count": 2,
    "items_count": 2,
    "items": [
      {
        "se_type": "google",
        "app_id": "com.facebook.katana",
        "metrics": {
          "google_play_search_organic": {
            "pos_1": 15157,
            "pos_2_3": 12317,
            "pos_4_10": 71802,
            "pos_11_100": 108436,
            "count": 207712,
            "search_volume": 44644191
          }
        }
   
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

- `dataforseo_merchant_google_products`
- `dataforseo_app_google_info`
- `dataforseo_app_google_searches`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
