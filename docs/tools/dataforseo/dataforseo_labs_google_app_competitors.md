---
name: dataforseo_labs_google_app_competitors
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_google_app_competitors`

Identify competitor apps on Google Play by keyword intersection — apps that rank for many of the same keywords as the target app.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `competitors`, `dataforseo`, `google` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_google_app_competitors",
  "params": {
    "app_id": "com.example.app"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `app_id` | string | yes |  | Google Play app ID (e.g. 'org.telegram.messenger'). |
| `location_name` | string | no |  | Location name. Required if location_code omitted. Currently US only. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `filters` | any[] | no |  | Filtering rules (up to 8). Example: ['intersections','>',500]. |
| `order_by` | any[] | no |  | Sorting rules (up to 3). Default: ['intersections,desc']. |
| `limit` | integer | no |  | Max apps returned (default 100, max 1000). |
| `offset` | integer | no |  | Result offset for pagination (default 0). |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "app_id": {
      "type": "string",
      "description": "Google Play app ID (e.g. 'org.telegram.messenger')."
    },
    "location_name": {
      "type": "string",
      "description": "Location name. Required if location_code omitted. Currently US only."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840). Required if location_name omitted."
    },
    "language_name": {
      "type": "string",
      "description": "Language name (e.g. 'English'). Required if language_code omitted."
    },
    "language_code": {
      "type": "string",
      "description": "Language code (e.g. 'en'). Required if language_name omitted."
    },
    "filters": {
      "type": "array",
      "description": "Filtering rules (up to 8). Example: ['intersections','>',500]."
    },
    "order_by": {
      "type": "array",
      "description": "Sorting rules (up to 3). Default: ['intersections,desc']."
    },
    "limit": {
      "type": "integer",
      "description": "Max apps returned (default 100, max 1000)."
    },
    "offset": {
      "type": "integer",
      "description": "Result offset for pagination (default 0)."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `dataforseo_labs/google/app_competitors/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "app_id"
  ]
}
```

## Example request

```json
{
  "app_id": "com.example.app"
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].se_type` | string |  |
| `[].app_id` | string |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].total_count` | integer |  |
| `[].items_count` | integer |  |
| `[].items[]` | array<object> |  |
| `[].items[].se_type` | string |  |
| `[].items[].app_id` | string |  |
| `[].items[].avg_position` | number |  |
| `[].items[].sum_position` | integer |  |
| `[].items[].intersections` | integer |  |
| `[].items[].competitor_metrics` | object |  |
| `[].items[].competitor_metrics.google_play_search_organic` | object |  |
| `[].items[].competitor_metrics.google_play_search_organic.pos_1` | integer |  |
| `[].items[].competitor_metrics.google_play_search_organic.pos_2_3` | integer |  |
| `[].items[].competitor_metrics.google_play_search_organic.pos_4_10` | integer |  |
| `[].items[].competitor_metrics.google_play_search_organic.pos_11_100` | integer |  |
| `[].items[].competitor_metrics.google_play_search_organic.count` | integer |  |
| `[].items[].competitor_metrics.google_play_search_organic.search_volume` | integer |  |
| `[].items[].full_metrics` | object |  |
| `[].items[].full_metrics.google_play_search_organic` | object |  |
| `[].items[].full_metrics.google_play_search_organic.pos_1` | integer |  |
| `[].items[].full_metrics.google_play_search_organic.pos_2_3` | integer |  |

### Example response (from profile)

```json
[
  {
    "se_type": "google",
    "app_id": "com.instagram.android",
    "location_code": 2840,
    "language_code": "en",
    "total_count": 177167,
    "items_count": 100,
    "items": [
      {
        "se_type": "google",
        "app_id": "com.instagram.android",
        "avg_position": 11.890420570994197,
        "sum_position": 2440164,
        "intersections": 205221,
        "competitor_metrics": {
          "google_play_search_organic": {
            "pos_1": 13379,
            "pos_2
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

**Chain inputs:** `{'param': 'app_id', 'from_tool': 'google_play_store', 'extract': '_custom_gplay_id'}`

**Chain groups:** `dataforseo_labs_appstore`

## Alternatives

- `dataforseo_merchant_google_products`
- `dataforseo_merchant_google_sellers`
- `dataforseo_app_google_info`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
