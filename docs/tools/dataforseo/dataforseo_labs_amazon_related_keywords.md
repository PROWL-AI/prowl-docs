---
name: dataforseo_labs_amazon_related_keywords
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_amazon_related_keywords`

Expand an Amazon seed keyword into related and long-tail keyword ideas.

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
  "tool_name": "dataforseo_labs_amazon_related_keywords",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keyword` | string | yes |  | Seed keyword to expand. UTF-8 encoding. |
| `location_name` | string | no |  | Amazon marketplace location (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `depth` | integer | no |  | Keyword expansion depth (default 1). Higher values return more results but cost more. |
| `include_seed_keyword` | boolean | no |  | If true, include the seed keyword in results. |
| `ignore_synonyms` | boolean | no |  | If true, return only core keywords (no near-synonyms). |
| `limit` | integer | no |  | Max keywords returned (default 100, max 1000). |
| `offset` | integer | no |  | Result offset for pagination (default 0). |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keyword": {
      "type": "string",
      "description": "Seed keyword to expand. UTF-8 encoding."
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
    "depth": {
      "type": "integer",
      "description": "Keyword expansion depth (default 1). Higher values return more results but cost more."
    },
    "include_seed_keyword": {
      "type": "boolean",
      "description": "If true, include the seed keyword in results."
    },
    "ignore_synonyms": {
      "type": "boolean",
      "description": "If true, return only core keywords (no near-synonyms)."
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
  "description": "Parameters for the DataForSEO `dataforseo_labs/amazon/related_keywords/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "keyword"
  ]
}
```

## Example request

```json
{
  "keyword": "example query"
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].se_type` | string |  |
| `[].seed_keyword` | string |  |
| `[].seed_keyword_data` | null |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].total_count` | integer |  |
| `[].items_count` | integer |  |
| `[].items[]` | array<object> |  |
| `[].items[].se_type` | string |  |
| `[].items[].keyword_data` | object |  |
| `[].items[].keyword_data.se_type` | string |  |
| `[].items[].keyword_data.keyword` | string |  |
| `[].items[].keyword_data.location_code` | integer |  |
| `[].items[].keyword_data.language_code` | string |  |
| `[].items[].keyword_data.keyword_info` | object |  |
| `[].items[].keyword_data.keyword_info.se_type` | string |  |
| `[].items[].keyword_data.keyword_info.last_updated_time` | string |  |
| `[].items[].keyword_data.keyword_info.search_volume` | integer |  |
| `[].items[].depth` | integer |  |
| `[].items[].related_keywords[]` | array<string> |  |

### Example response (from profile)

```json
[
  {
    "se_type": "amazon",
    "seed_keyword": "instagram",
    "seed_keyword_data": null,
    "location_code": 2840,
    "language_code": "en",
    "total_count": 7,
    "items_count": 7,
    "items": [
      {
        "se_type": "amazon",
        "keyword_data": {
          "se_type": "amazon",
          "keyword": "instagram",
          "location_code": 2840,
          "language_code": "en",
          "keyword_info": {
            "se_type": "amazon",
            "last_updated_time": "202
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

- `dataforseo_labs_amazon_product_keyword_intersections`
- `dataforseo_merchant_amazon_products`
- `dataforseo_merchant_amazon_sellers`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
