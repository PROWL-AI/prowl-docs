---
name: ebay_product
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `ebay_product`

eBay Product — detailed product info from eBay.

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
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "ebay_product",
  "params": {
    "product_id": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `product_id` | string | yes |  | eBay product ID |
| `ebay_domain` | string | no |  | eBay domain |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "eBay product ID"
    },
    "ebay_domain": {
      "type": "string",
      "description": "eBay domain"
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

Top-level keys: `search_metadata`, `search_parameters`, `error`

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
| `search_parameters.ebay_domain` | string |  |
| `search_parameters.country` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_16dWXw4JOrIVd0DVgvqoKNGl",
    "status": "Success",
    "created_at": "2026-03-28T22:01:37Z",
    "request_time_taken": 0.49,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.49,
    "request_url": "https://www.ebay.com/p/376731240436",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_16dWXw4JOrIVd0DVgvqoKNGl.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_16dWXw4JOrIVd0DVgvqoKNGl"
  },
  "search_parameter
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

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'ebay_search', 'extract': '_custom_ebay_id'}`

**Chain groups:** `searchapi_ecommerce`

## Alternatives

- `serpapi_ebay_product`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
