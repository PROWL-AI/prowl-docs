---
name: dataforseo_keywords_bing_keyword_performance
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_keywords_bing_keyword_performance`

Return impressions, clicks, CTR, average CPC, and total spend for up to 1000 Bing keywords.

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
  "tool_name": "dataforseo_keywords_bing_keyword_performance",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | any[] | yes |  | Target keywords (up to 1000). UTF-8; converted to lowercase. Max 80 characters and 10 words per keyword phrase. |
| `location_name` | string | no |  | Full location name (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840 for US). Required if location_name omitted. |
| `language_name` | string | no |  | Full language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `device` | enum(all, desktop, mobile, tablet) | no |  | Device type filter. Possible values: all, desktop, mobile, tablet. Default: all. |
| `match` | string | no |  | Keyword match type. Possible values: aggregate, broad, phrase, exact. Default: aggregate (data across all match types). |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "description": "Target keywords (up to 1000). UTF-8; converted to lowercase. Max 80 characters and 10 words per keyword phrase."
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States'). Required if location_code omitted."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840 for US). Required if location_name omitted."
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
      "description": "Device type filter. Possible values: all, desktop, mobile, tablet. Default: all.",
      "enum": [
        "all",
        "desktop",
        "mobile",
        "tablet"
      ]
    },
    "match": {
      "type": "string",
      "description": "Keyword match type. Possible values: aggregate, broad, phrase, exact. Default: aggregate (data across all match types)."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `keywords_data/bing/keyword_performance/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
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
| `[].year` | integer |  |
| `[].month` | integer |  |
| `[].keyword_kpi` | object |  |
| `[].keyword_kpi.desktop[]` | array<object> |  |
| `[].keyword_kpi.desktop[].ad_position` | string |  |
| `[].keyword_kpi.desktop[].clicks` | integer |  |
| `[].keyword_kpi.desktop[].impressions` | integer |  |
| `[].keyword_kpi.desktop[].average_cpc` | number |  |
| `[].keyword_kpi.desktop[].ctr` | number |  |
| `[].keyword_kpi.desktop[].total_cost` | number |  |
| `[].keyword_kpi.desktop[].average_bid` | number |  |
| `[].keyword_kpi.mobile[]` | array<object> |  |
| `[].keyword_kpi.mobile[].ad_position` | string |  |
| `[].keyword_kpi.mobile[].clicks` | integer |  |
| `[].keyword_kpi.mobile[].impressions` | integer |  |
| `[].keyword_kpi.mobile[].average_cpc` | number |  |
| `[].keyword_kpi.mobile[].ctr` | number |  |
| `[].keyword_kpi.mobile[].total_cost` | number |  |
| `[].keyword_kpi.mobile[].average_bid` | number |  |
| `[].keyword_kpi.tablet[]` | array<object> |  |
| `[].keyword_kpi.tablet[].ad_position` | string |  |

### Example response (from profile)

```json
[
  {
    "keyword": "instagram",
    "location_code": 2840,
    "language_code": "en",
    "year": 2026,
    "month": 7,
    "keyword_kpi": {
      "desktop": [
        {
          "ad_position": "MainLine1",
          "clicks": 48,
          "impressions": 355,
          "average_cpc": 0.280625,
          "ctr": 13.521126747131348,
          "total_cost": 13.47,
          "average_bid": 1.06481690140845
        },
        {
          "ad_position": "MainLine2",
          "clicks": 16,
        
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

- `dataforseo_ai_keyword_volume`
- `dataforseo_labs_amazon_product_keyword_intersections`
- `dataforseo_labs_amazon_related_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
