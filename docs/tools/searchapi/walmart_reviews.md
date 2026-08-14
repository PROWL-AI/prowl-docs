---
name: walmart_reviews
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `walmart_reviews`

Walmart Reviews — product reviews from Walmart.

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
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "walmart_reviews",
  "params": {
    "product_id": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `product_id` | string | yes |  | Walmart product ID |
| `page` | integer | no |  | Page number (for pagination) |
| `sort_by` | enum(relevancy, submission-desc, submission-asc, rating-desc, rating-asc) | no |  | Sort reviews |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Walmart product ID"
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
    },
    "sort_by": {
      "type": "string",
      "description": "Sort reviews",
      "enum": [
        "relevancy",
        "submission-desc",
        "submission-asc",
        "rating-desc",
        "rating-asc"
      ]
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

Top-level keys: `search_metadata`, `search_parameters`, `product`

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
| `product` | object |  |
| `product.title` | string |  |
| `product.link` | string |  |
| `product.reviews_count` | integer |  |
| `product.reviews_with_text_count` | integer |  |
| `product.reviews_histogram` | object |  |
| `product.reviews_histogram.1` | object |  |
| `product.reviews_histogram.2` | object |  |
| `product.reviews_histogram.3` | object |  |
| `product.reviews_histogram.4` | object |  |
| `product.reviews_histogram.5` | object |  |
| `product.recommended_percentage` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_JoY68Me7qNsAjLLz3v0axRVb",
    "status": "Success",
    "created_at": "2026-03-28T21:56:23Z",
    "request_time_taken": 2.02,
    "parsing_time_taken": 0.0,
    "total_time_taken": 2.02,
    "request_url": "https://www.walmart.com/reviews/product/24ZW0R1JWQIV",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_JoY68Me7qNsAjLLz3v0axRVb.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_JoY68Me7qNsAjLLz3v0axRVb"
  },
  
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

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'walmart_search', 'extract': 'organic_results[].product_id'}`

**Chain groups:** `searchapi_ecommerce`

## Alternatives

- `serpapi_walmart_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
