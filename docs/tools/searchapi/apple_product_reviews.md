---
name: apple_product_reviews
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `apple_product_reviews`

Apple Product Reviews — app reviews from the App Store.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `reviews`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "apple_product_reviews",
  "params": {
    "product_id": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `product_id` | string | yes |  | Apple app ID |
| `country` | string | no |  | Store country code (e.g. 'us', 'gb') |
| `sort_by` | enum(most_recent, most_helpful) | no |  | Sort reviews |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Apple app ID"
    },
    "country": {
      "type": "string",
      "description": "Store country code (e.g. 'us', 'gb')"
    },
    "sort_by": {
      "type": "string",
      "description": "Sort reviews",
      "enum": [
        "most_recent",
        "most_helpful"
      ]
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
    }
  },
  "required": [
    "product_id"
  ]
}
```

## Example request

```json
{
  "product_id": "B08N5WRWNW"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `reviews`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.request_time_taken` | number |  |
| `search_metadata.parsing_time_taken` | number |  |
| `search_metadata.total_time_taken` | number |  |
| `search_metadata.request_url` | string |  |
| `search_metadata.html_url` | string |  |
| `search_metadata.json_url` | string |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.product_id` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.page` | integer |  |
| `search_parameters.sort_by` | string |  |
| `reviews[]` | array<object> |  |
| `reviews[].id` | string |  |
| `reviews[].title` | string |  |
| `reviews[].text` | string |  |
| `reviews[].rating` | integer |  |
| `reviews[].review_date` | string |  |
| `reviews[].version` | string |  |
| `reviews[].author` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_MG6OPWeEVjFx9wKy94jR8w7N",
    "status": "Success",
    "created_at": "2026-03-28T21:55:34Z",
    "request_time_taken": 0.86,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.86,
    "request_url": "https://apps.apple.com/us/app/id389801252?see-all=reviews",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9wKy94jR8w7N.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9wKy94jR8w7N"
  
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SEARCH_API_KEY | Skip SearchAPI tools — use Exa or Perplexity as alternatives for web search |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 422 | Invalid parameters | Check query and filter parameters match the expected format |

## When to use

- Engine-specific SearchAPI surface — pass marketplace/locale params when the schema exposes them
- ID-like params (property_id, asin, place_id) must be real identifiers from a prior search tool

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'apple_app_store', 'extract': 'organic_results[].id'}`

**Chain groups:** `searchapi_appstores`

## Alternatives

- `google_play_product_reviews`
- `scrape_review_platforms`
- `serpapi_apple_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
