---
name: dataforseo_labs_amazon_product_rank_overview
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_amazon_product_rank_overview`

Get an organic keyword ranking overview for up to 1000 Amazon ASINs in bulk.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `amazon`, `dataforseo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_amazon_product_rank_overview",
  "params": {
    "asins": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asins` | any[] | yes |  | Amazon ASINs to analyse (up to 1000). E.g. ['B08N5WRWNW']. |
| `location_name` | string | no |  | Amazon marketplace location (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "asins": {
      "type": "array",
      "description": "Amazon ASINs to analyse (up to 1000). E.g. ['B08N5WRWNW']."
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
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `dataforseo_labs/amazon/product_rank_overview/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "asins"
  ]
}
```

## Example request

```json
{
  "asins": []
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
| `[].items[].asin` | string |  |
| `[].items[].metrics` | object |  |
| `[].items[].metrics.amazon_serp` | object |  |
| `[].items[].metrics.amazon_serp.pos_1` | integer |  |
| `[].items[].metrics.amazon_serp.pos_2_3` | integer |  |
| `[].items[].metrics.amazon_serp.pos_4_10` | integer |  |
| `[].items[].metrics.amazon_serp.pos_11_100` | integer |  |
| `[].items[].metrics.amazon_serp.count` | integer |  |
| `[].items[].metrics.amazon_serp.search_volume` | integer |  |
| `[].items[].metrics.amazon_paid` | object |  |
| `[].items[].metrics.amazon_paid.pos_1` | integer |  |
| `[].items[].metrics.amazon_paid.pos_2_3` | integer |  |
| `[].items[].metrics.amazon_paid.pos_4_10` | integer |  |
| `[].items[].metrics.amazon_paid.pos_11_100` | integer |  |
| `[].items[].metrics.amazon_paid.count` | integer |  |
| `[].items[].metrics.amazon_paid.search_volume` | integer |  |

### Example response (from profile)

```json
[
  {
    "se_type": "amazon",
    "location_code": 2840,
    "language_code": "en",
    "total_count": 1,
    "items_count": 1,
    "items": [
      {
        "se_type": "amazon",
        "asin": "B01LW2SL7R",
        "metrics": {
          "amazon_serp": {
            "pos_1": 3,
            "pos_2_3": 4,
            "pos_4_10": 21,
            "pos_11_100": 93,
            "count": 121,
            "search_volume": 8607
          },
          "amazon_paid": {
            "pos_1": 0,
         
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

- `dataforseo_merchant_amazon_products`
- `dataforseo_merchant_amazon_sellers`
- `dataforseo_labs_amazon_bulk_search_volume`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
