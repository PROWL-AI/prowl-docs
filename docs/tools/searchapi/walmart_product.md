---
name: walmart_product
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `walmart_product`

Walmart Product — detailed product info from Walmart.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "walmart_product",
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

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Walmart product ID"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `product`, `reviews`

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
| `search_information` | object |  |
| `search_information.meta_title` | string |  |
| `search_information.meta_description` | string |  |
| `search_information.postal_code` | string |  |
| `search_information.province_code` | string |  |
| `search_information.city` | string |  |
| `search_information.store_id` | string |  |
| `product` | object |  |
| `product.id` | string |  |
| `product.product_id` | string |  |
| `product.upc` | string |  |
| `product.title` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_1g3L6weL3bSxlPYgjkpaP2rB",
    "status": "Success",
    "created_at": "2026-03-28T21:56:20Z",
    "request_time_taken": 2.29,
    "parsing_time_taken": 0.01,
    "total_time_taken": 2.3,
    "request_url": "https://www.walmart.com/ip/24ZW0R1JWQIV",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_1g3L6weL3bSxlPYgjkpaP2rB.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_1g3L6weL3bSxlPYgjkpaP2rB"
  },
  "search_param
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

- `serpapi_walmart_product`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
