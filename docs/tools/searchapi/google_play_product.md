---
name: google_play_product
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_play_product`

Google Play Product — detailed Android app info (description, ratings, downloads, developer).

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
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_play_product",
  "params": {
    "product_id": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `product_id` | string | yes |  | App package name (e.g. 'com.example.app') |
| `store` | enum(apps, games) | no | `apps` | Store type |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "App package name (e.g. 'com.example.app')"
    },
    "store": {
      "type": "string",
      "description": "Store type",
      "enum": [
        "apps",
        "games"
      ],
      "default": "apps"
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

Top-level keys: `search_metadata`, `search_parameters`, `product`, `media`, `data_safety`, `additional_information`, `similar_products`, `reviews`, `reviews_pagination`

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
| `search_parameters.store` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.product_id` | string |  |
| `search_parameters.num` | integer |  |
| `product` | object |  |
| `product.title` | string |  |
| `product.product_id` | string |  |
| `product.authors[]` | array<object> |  |
| `product.developer_contact` | object |  |
| `product.developer_contact.website` | string |  |
| `product.developer_contact.email` | string |  |
| `product.developer_contact.privacy_policy` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_mMjwVJvBznTROJmP1vynp5OY",
    "status": "Success",
    "created_at": "2026-03-28T22:01:33Z",
    "request_time_taken": 1.64,
    "parsing_time_taken": 0.02,
    "total_time_taken": 1.66,
    "request_url": "https://play.google.com/store/apps/details?id=com.instagram.android&hl=en&gl=us",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_mMjwVJvBznTROJmP1vynp5OY.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_mMjwV
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

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'google_play_store', 'extract': '_custom_gplay_id'}`

**Chain groups:** `searchapi_appstores`

## Alternatives

- `google_about_this_domain`
- `google_ads_advertiser_info`
- `google_ads_transparency_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
