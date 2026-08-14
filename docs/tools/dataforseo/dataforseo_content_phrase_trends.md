---
name: dataforseo_content_phrase_trends
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_content_phrase_trends`

Get citation trends over time for a keyword — track mention volume changes.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `trends` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_content_phrase_trends",
  "params": {
    "date_from": "YYYY-MM-DD",
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `date_group` | enum(day, week, month) | no |  | time range which will be used to group the results |
| `initial_dataset_filters` | any[] | no |  | initial dataset filtering parameters |
| `internal_list_limit` | integer | no |  | maximum number of elements within internal arrays |
| `keyword_fields` | string | no |  | target keyword fields and target keywords |
| `page_type` | any[] | no |  | target page types |
| `rank_scale` | string | no |  | defines the scale used for calculating and displaying the rank values |
| `search_mode` | string | no |  | results grouping type |
| `tag` | string | no |  | user-defined task identifier |
| `keyword` | string | yes |  | Search keyword or query |
| `date_from` | string | yes |  | Start date (YYYY-MM-DD) |
| `date_to` | string | no |  | End date (YYYY-MM-DD) |
| `filters` | any[] | no |  | DataForSEO filter conditions array |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "date_group": {
      "type": "string",
      "description": "time range which will be used to group the results",
      "enum": [
        "day",
        "week",
        "month"
      ]
    },
    "initial_dataset_filters": {
      "type": "array",
      "description": "initial dataset filtering parameters"
    },
    "internal_list_limit": {
      "type": "integer",
      "description": "maximum number of elements within internal arrays"
    },
    "keyword_fields": {
      "type": "string",
      "description": "target keyword fields and target keywords"
    },
    "page_type": {
      "type": "array",
      "description": "target page types"
    },
    "rank_scale": {
      "type": "string",
      "description": "defines the scale used for calculating and displaying the rank values"
    },
    "search_mode": {
      "type": "string",
      "description": "results grouping type"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "keyword": {
      "type": "string",
      "description": "Search keyword or query"
    },
    "date_from": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD)"
    },
    "date_to": {
      "type": "string",
      "description": "End date (YYYY-MM-DD)"
    },
    "filters": {
      "type": "array",
      "description": "DataForSEO filter conditions array"
    }
  },
  "required": [
    "keyword",
    "date_from"
  ]
}
```

## Example request

```json
{
  "date_from": "YYYY-MM-DD",
  "keyword": "example query"
}
```

## Output

_No output schema or active profile response_format._

> Profile capture status: **error** — DataForSEOError: DataForSEO task errors: 40501: Invalid Field: 'date_from'.

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

- `google_trends`
- `google_trends_autocomplete`
- `serpapi_google_trends`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
