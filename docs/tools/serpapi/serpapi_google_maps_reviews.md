---
name: serpapi_google_maps_reviews
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_maps_reviews`

Google Maps Reviews via SerpAPI — reviews for a specific place by data_id.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `maps`, `reviews`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_maps_reviews",
  "params": {
    "data_id": "data_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `data_id` | string | yes |  | Place data_id from Google Maps results |
| `hl` | string | no | `en` | Language code (default 'en') |
| `sort_by` | enum(qualityScore, newestFirst, ratingHigh, ratingLow) | no |  | Sort order |
| `next_page_token` | string | no |  | Pagination token |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "data_id": {
      "type": "string",
      "description": "Place data_id from Google Maps results"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "sort_by": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "qualityScore",
        "newestFirst",
        "ratingHigh",
        "ratingLow"
      ]
    },
    "next_page_token": {
      "type": "string",
      "description": "Pagination token"
    }
  },
  "required": [
    "data_id"
  ]
}
```

## Example request

```json
{
  "data_id": "data_id_example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `place_info`, `topics`, `reviews`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_maps_reviews_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.data_id` | string |  |
| `search_parameters.hl` | string |  |
| `place_info` | object |  |
| `place_info.title` | string |  |
| `place_info.address` | string |  |
| `place_info.rating` | number |  |
| `place_info.reviews` | integer |  |
| `place_info.type` | string |  |
| `topics[]` | array<object> |  |
| `topics[].keyword` | string |  |
| `topics[].mentions` | integer |  |
| `topics[].id` | string |  |
| `reviews[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c8501e71577fa59f07719e",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/GNgPq57QJCd-Gwip-rhPJg/69c8501e71577fa59f07719e.json",
    "created_at": "2026-03-28 22:03:10 UTC",
    "processed_at": "2026-03-28 22:03:10 UTC",
    "google_maps_reviews_url": "https://www.google.com/maps/place/data=!4m7!3m6!1s0x89c2590b5700aed3:0x143482a9c81bf22b!5m2!4m1!1i2!9m1!1b1?hl=en",
    "raw_html_file": "https://serpapi.com/searches/GNgPq57QJCd-Gwi
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SERP_API_KEY | Check SERP_API_KEY in .env or SerpAPI dashboard |
| 429 | Monthly rate limit reached | Upgrade SerpAPI plan or wait for quota reset |
| 400 | Missing required parameters | Check query and engine parameters |

## When to use

- SerpAPI engine is encoded in the tool name — do not re-pass engine unless the schema requires it
- Prefer the SearchAPI twin when cost/coverage is better for the same surface
- Paginate with num/start (or page) when result sets are truncated

**Chain inputs:** `{'param': 'data_id', 'from_tool': 'serpapi_google_maps', 'extract': 'local_results[].data_id'}`

**Chain groups:** `serpapi_places`

## Alternatives

- `google_maps_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
