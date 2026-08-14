---
name: dataforseo_keywords_bing_search_volume_history
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_keywords_bing_search_volume_history`

Retrieve historical Bing search volume for up to 1000 keywords broken down by weekly or monthly periods.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `history`, `keywords`, `search` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_keywords_bing_search_volume_history",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | any[] | yes |  | Target keywords (up to 1000). UTF-8; converted to lowercase. |
| `location_name` | string | no |  | Full location name (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Full language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `device` | enum(all, desktop, mobile, tablet) | no |  | Device type: all, desktop, mobile, tablet. Default: all. |
| `period` | string | no |  | Aggregation period: 'monthly' or 'weekly'. Default: monthly. |
| `date_from` | string | no |  | Start of historical range (yyyy-mm-dd). Min: 24 months ago. |
| `date_to` | string | no |  | End of historical range (yyyy-mm-dd). Max: one month from today. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "description": "Target keywords (up to 1000). UTF-8; converted to lowercase."
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States'). Required if location_code omitted."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840). Required if location_name omitted."
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English'). Required if language_code omitted."
    },
    "language_code": {
      "type": "string",
      "description": "Language code (e.g. 'en'). Required if language_name omitted."
    },
    "device": {
      "type": "string",
      "description": "Device type: all, desktop, mobile, tablet. Default: all.",
      "enum": [
        "all",
        "desktop",
        "mobile",
        "tablet"
      ]
    },
    "period": {
      "type": "string",
      "description": "Aggregation period: 'monthly' or 'weekly'. Default: monthly."
    },
    "date_from": {
      "type": "string",
      "description": "Start of historical range (yyyy-mm-dd). Min: 24 months ago."
    },
    "date_to": {
      "type": "string",
      "description": "End of historical range (yyyy-mm-dd). Max: one month from today."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `keywords_data/bing/search_volume_history/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": []
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].keyword` | string |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].device[]` | array<string> |  |
| `[].period` | string |  |
| `[].searches` | object |  |
| `[].searches.desktop[]` | array<object> |  |
| `[].searches.desktop[].year` | integer |  |
| `[].searches.desktop[].month` | integer |  |
| `[].searches.desktop[].day` | integer |  |
| `[].searches.desktop[].search_volume` | integer |  |
| `[].searches.non_smartphones` | null |  |
| `[].searches.mobile[]` | array<object> |  |
| `[].searches.mobile[].year` | integer |  |
| `[].searches.mobile[].month` | integer |  |
| `[].searches.mobile[].day` | integer |  |
| `[].searches.mobile[].search_volume` | integer |  |
| `[].searches.tablet[]` | array<object> |  |
| `[].searches.tablet[].year` | integer |  |
| `[].searches.tablet[].month` | integer |  |
| `[].searches.tablet[].day` | integer |  |
| `[].searches.tablet[].search_volume` | integer |  |

### Example response (from profile)

```json
[
  {
    "keyword": "instagram",
    "location_code": 2840,
    "language_code": "en",
    "device": [
      "desktop",
      "non_smartphones",
      "mobile",
      "tablet"
    ],
    "period": "monthly",
    "searches": {
      "desktop": [
        {
          "year": 2026,
          "month": 7,
          "day": 1,
          "search_volume": 6157252
        },
        {
          "year": 2026,
          "month": 6,
          "day": 1,
          "search_volume": 6083535
        },
        {

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

- `exa_keyword_search`
- `majestic_search_by_keyword`
- `dataforseo_app_apple_searches`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
