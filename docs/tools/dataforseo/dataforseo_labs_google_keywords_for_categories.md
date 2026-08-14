---
name: dataforseo_labs_google_keywords_for_categories
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_google_keywords_for_categories`

Return keyword ideas for up to 20 Google product/service category codes.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_google_keywords_for_categories",
  "params": {
    "category_codes": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `category_codes` | any[] | yes |  | Product/service category codes (up to 20). Download full list from DataForSEO. |
| `location_name` | string | no |  | Location name (e.g. 'United States'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `language_name` | string | no |  | Language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | Language code (e.g. 'en'). Required if language_name omitted. |
| `limit` | integer | no |  | Max keywords returned (default 100, max 1000). |
| `offset` | integer | no |  | Result offset for pagination (default 0). |
| `offset_token` | string | no |  | Pagination token for retrieving over 10 000 results. |
| `filters` | any[] | no |  | Filtering rules (up to 8). Example: ['keyword_info.search_volume','>',0]. |
| `order_by` | any[] | no |  | Sorting rules (up to 3). Example: ['keyword_info.search_volume,desc']. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "category_codes": {
      "type": "array",
      "description": "Product/service category codes (up to 20). Download full list from DataForSEO."
    },
    "location_name": {
      "type": "string",
      "description": "Location name (e.g. 'United States'). Required if location_code omitted."
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
    "limit": {
      "type": "integer",
      "description": "Max keywords returned (default 100, max 1000)."
    },
    "offset": {
      "type": "integer",
      "description": "Result offset for pagination (default 0)."
    },
    "offset_token": {
      "type": "string",
      "description": "Pagination token for retrieving over 10 000 results."
    },
    "filters": {
      "type": "array",
      "description": "Filtering rules (up to 8). Example: ['keyword_info.search_volume','>',0]."
    },
    "order_by": {
      "type": "array",
      "description": "Sorting rules (up to 3). Example: ['keyword_info.search_volume,desc']."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `dataforseo_labs/google/keywords_for_categories/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "category_codes"
  ]
}
```

## Example request

```json
{
  "category_codes": []
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].se_type` | string |  |
| `[].seed_categories[]` | array<integer> |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].total_count` | integer |  |
| `[].items_count` | integer |  |
| `[].offset` | integer |  |
| `[].offset_token` | string |  |
| `[].items[]` | array<object> |  |
| `[].items[].se_type` | string |  |
| `[].items[].keyword` | string |  |
| `[].items[].location_code` | integer |  |
| `[].items[].language_code` | string |  |
| `[].items[].keyword_info` | object |  |
| `[].items[].keyword_info.se_type` | string |  |
| `[].items[].keyword_info.last_updated_time` | string |  |
| `[].items[].keyword_info.competition` | number |  |
| `[].items[].keyword_info.competition_level` | string |  |
| `[].items[].keyword_info.cpc` | number |  |
| `[].items[].keyword_info.search_volume` | integer |  |
| `[].items[].keyword_info.low_top_of_page_bid` | number |  |
| `[].items[].keyword_info.high_top_of_page_bid` | number |  |
| `[].items[].keyword_info.categories[]` | array<integer> |  |
| `[].items[].keyword_info.monthly_searches[]` | array<object> |  |

### Example response (from profile)

```json
[
  {
    "se_type": "google",
    "seed_categories": [
      10021
    ],
    "location_code": 2840,
    "language_code": "en",
    "total_count": 38644904,
    "items_count": 100,
    "offset": 0,
    "offset_token": "eyJDdXJyZW50T2Zmc2V0IjoxMDAsIlJlcXVlc3REYXRhIjp7ImNhdGVnb3JpZXMiOlsxMDAyMV0sImxvY2F0aW9uIjoyODQwLCJsYW5ndWFnZSI6ImVuIiwiaW50ZXJzZWN0Ijp0cnVlLCJsb2FkX3NlcnBfaW5mbyI6ZmFsc2UsInNlYXJjaF9hZnRlcl90b2tlbiI6bnVsbCwiaWdub3JlX3N5bm9ueW1zIjpmYWxzZSwic2VhcmNoX2VuZ2luZSI6Imdvb2dsZSIsInVzZV9u
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

- `dataforseo_labs_google_categories_for_keywords`
- `dataforseo_kw_google_ads_keywords_for_keywords`
- `dataforseo_kw_google_ads_keywords_for_site`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
