---
name: dataforseo_keywords_bing_keywords_for_keywords
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_keywords_bing_keywords_for_keywords`

Expand up to 1000 Bing seed keywords into related keyword ideas with search volume, CPC, and competition data.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_keywords_bing_keywords_for_keywords",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | any[] | yes |  | Seed keywords to expand (up to 1000). UTF-8; converted to lowercase. |
| `location_name` | string | no |  | Full location name (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Full language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `sort_by` | string | no |  | Sort results by: relevance, search_volume, cpc, competition. Default: relevance. |
| `keywords_negative` | any[] | no |  | Negative keywords to exclude from suggestions (up to 200). |
| `device` | enum(all, desktop, mobile, tablet) | no |  | Device type: all, desktop, mobile, tablet. Default: all. |
| `date_from` | string | no |  | Start of date range (yyyy-mm-dd). Min: 24 months ago. Default: last 12 months. |
| `date_to` | string | no |  | End of date range (yyyy-mm-dd). Default: last 12 months. |
| `search_partners` | boolean | no |  | If true, include Bing's owned/operated/syndicated partner networks (Yahoo, AOL, etc.). Default: false. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "description": "Seed keywords to expand (up to 1000). UTF-8; converted to lowercase."
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
    "sort_by": {
      "type": "string",
      "description": "Sort results by: relevance, search_volume, cpc, competition. Default: relevance."
    },
    "keywords_negative": {
      "type": "array",
      "description": "Negative keywords to exclude from suggestions (up to 200)."
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
    "date_from": {
      "type": "string",
      "description": "Start of date range (yyyy-mm-dd). Min: 24 months ago. Default: last 12 months."
    },
    "date_to": {
      "type": "string",
      "description": "End of date range (yyyy-mm-dd). Default: last 12 months."
    },
    "search_partners": {
      "type": "boolean",
      "description": "If true, include Bing's owned/operated/syndicated partner networks (Yahoo, AOL, etc.). Default: false."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `keywords_data/bing/keywords_for_keywords/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
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
| `[].search_partners` | boolean |  |
| `[].device` | string |  |
| `[].competition` | number |  |
| `[].cpc` | number |  |
| `[].search_volume` | integer |  |
| `[].categories` | null |  |
| `[].monthly_searches[]` | array<object> |  |
| `[].monthly_searches[].year` | integer |  |
| `[].monthly_searches[].month` | integer |  |
| `[].monthly_searches[].search_volume` | integer |  |

### Example response (from profile)

```json
[
  {
    "keyword": "instagram",
    "location_code": 2840,
    "language_code": "en",
    "search_partners": false,
    "device": "all",
    "competition": 0.9,
    "cpc": 0.24,
    "search_volume": 4570300,
    "categories": null,
    "monthly_searches": [
      {
        "year": 2026,
        "month": 7,
        "search_volume": 4605250
      },
      {
        "year": 2026,
        "month": 6,
        "search_volume": 4529750
      },
      {
        "year": 2026,
        "month": 5,
      
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

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
