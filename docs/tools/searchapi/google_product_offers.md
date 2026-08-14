---
name: google_product_offers
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_product_offers`

Google Product Offers — price comparison offers from multiple sellers for a product.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_product_offers",
  "params": {
    "product_token": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `product_token` | string | yes |  | Product token from google_shopping results |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_token": {
      "type": "string",
      "description": "Product token from google_shopping results"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    }
  },
  "required": [
    "product_token"
  ]
}
```

## Example request

```json
{
  "product_token": "example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `product`, `offers`, `pagination`

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
| `search_parameters.product_token` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.page` | integer |  |
| `search_information` | object |  |
| `search_information.total_offers` | integer |  |
| `product` | object |  |
| `product.title` | string |  |
| `product.link` | string |  |
| `offers[]` | array<object> |  |
| `offers[].position` | integer |  |
| `offers[].title` | string |  |
| `offers[].link` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_dXG2jzvrlqTobDDodeYoaOb8",
    "status": "Success",
    "created_at": "2026-03-28T21:56:33Z",
    "request_time_taken": 0.81,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.81,
    "request_url": "https://www.google.com/search?q=instagram+app&oq=instagram+app&gl=us&hl=en&udm=28#oshopproduct=oid:1583488521154569122,iid:1765908045719270699,pvt:hg,pvo:3&oshop=apv&pvs=0",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_dXG2jzvrlqT
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

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

**Chain inputs:** `{'param': 'product_token', 'from_tool': 'google_shopping', 'extract': 'shopping_results[].product_token'}`

**Chain groups:** `searchapi_shopping`

## Alternatives

- `google_about_this_domain`
- `google_ads_advertiser_info`
- `google_ads_transparency_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
