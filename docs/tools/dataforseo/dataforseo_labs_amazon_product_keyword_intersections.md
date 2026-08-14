---
name: dataforseo_labs_amazon_product_keyword_intersections
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_amazon_product_keyword_intersections`

Find organic keywords shared across multiple Amazon ASINs (up to 1000).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `amazon`, `dataforseo`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_amazon_product_keyword_intersections",
  "params": {
    "asins": {}
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asins` | object | yes |  | Dict of ASINs keyed by position string (up to 20). E.g. {'1':'B01LW2SL7R','2':'B0DCCYZ1K2'} — the intersection endpoint takes a position-keyed object, not an array. |
| `location_name` | string | no |  | Amazon marketplace location (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `intersection_mode` | string | no |  | 'union' (keywords in any ASIN) or 'intersection' (keywords in all ASINs). Default: 'union'. |
| `filters` | any[] | no |  | Filtering rules (up to 8). Example: ['keyword_data.keyword_info.search_volume','>',0]. |
| `order_by` | any[] | no |  | Sorting rules (up to 3). Default: ['keyword_data.keyword_info.search_volume,desc']. |
| `limit` | integer | no |  | Max keywords returned (default 100, max 1000). |
| `offset` | integer | no |  | Result offset for pagination (default 0). |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "asins": {
      "type": "object",
      "description": "Dict of ASINs keyed by position string (up to 20). E.g. {'1':'B01LW2SL7R','2':'B0DCCYZ1K2'} \u2014 the intersection endpoint takes a position-keyed object, not an array."
    },
    "location_name": {
      "type": "string",
      "description": "Amazon marketplace location (e.g. 'United States'). Required if location_code omitted."
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
    "intersection_mode": {
      "type": "string",
      "description": "'union' (keywords in any ASIN) or 'intersection' (keywords in all ASINs). Default: 'union'."
    },
    "filters": {
      "type": "array",
      "description": "Filtering rules (up to 8). Example: ['keyword_data.keyword_info.search_volume','>',0]."
    },
    "order_by": {
      "type": "array",
      "description": "Sorting rules (up to 3). Default: ['keyword_data.keyword_info.search_volume,desc']."
    },
    "limit": {
      "type": "integer",
      "description": "Max keywords returned (default 100, max 1000)."
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
  "description": "Parameters for the DataForSEO `dataforseo_labs/amazon/product_keyword_intersections/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "asins"
  ]
}
```

## Example request

```json
{
  "asins": {}
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].se_type` | string |  |
| `[].asins` | object |  |
| `[].asins.1` | string |  |
| `[].asins.2` | string |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].total_count` | null |  |
| `[].items_count` | integer |  |
| `[].items` | null |  |

### Example response (from profile)

```json
[
  {
    "se_type": "amazon",
    "asins": {
      "1": "B01LW2SL7R",
      "2": "B0DCCYZ1K2"
    },
    "location_code": 2840,
    "language_code": "en",
    "total_count": null,
    "items_count": 0,
    "items": null
  }
]
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

- `dataforseo_labs_amazon_related_keywords`
- `dataforseo_merchant_amazon_products`
- `dataforseo_merchant_amazon_sellers`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
