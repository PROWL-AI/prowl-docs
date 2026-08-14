---
name: serpapi_walmart_product
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_walmart_product`

Walmart product details via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_walmart_product",
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
| `store_id` | string | no |  | Walmart store id — price and stock are per store, so without it you get an arbitrary store's shelf. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Walmart product ID"
    },
    "store_id": {
      "type": "string",
      "description": "Walmart store id \u2014 price and stock are per store, so without it you get an arbitrary store's shelf."
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `product_result`, `reviews_results`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.walmart_product_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.product_id` | string |  |
| `search_parameters.engine` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.location` | object |  |
| `search_information.location.postal_code` | string |  |
| `search_information.location.province_code` | string |  |
| `search_information.location.city` | string |  |
| `search_information.location.store_id` | string |  |
| `product_result` | object |  |
| `product_result.us_item_id` | string |  |
| `product_result.product_id` | string |  |
| `product_result.variants[]` | array<string> |  |
| `product_result.upc` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c84ff0421b085992370094",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/UJtxMg3bDTDRUnUEMMlRKw/69c84ff0421b085992370094.json",
    "created_at": "2026-03-28 22:02:24 UTC",
    "processed_at": "2026-03-28 22:02:24 UTC",
    "walmart_product_url": "https://www.walmart.com/ip/6441553093?",
    "raw_html_file": "https://serpapi.com/searches/UJtxMg3bDTDRUnUEMMlRKw/69c84ff0421b085992370094.html",
    "prettify_html_file": "https://serp
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

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'serpapi_walmart', 'extract': 'organic_results[].us_item_id'}`

**Chain groups:** `serpapi_ecommerce`

## Alternatives

- `walmart_product`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
