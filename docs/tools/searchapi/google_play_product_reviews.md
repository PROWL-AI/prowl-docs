---
name: google_play_product_reviews
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_play_product_reviews`

Google Play Product Reviews — fetch user reviews for an Android app.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `reviews`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_play_product_reviews",
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
| `num` | integer | no | `200` | Number of reviews to return (default 200, max 200) |
| `next_page_token` | string | no |  | Token for fetching the next page of reviews |

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
    },
    "num": {
      "type": "integer",
      "description": "Number of reviews to return (default 200, max 200)",
      "minimum": 1,
      "maximum": 200,
      "default": 200
    },
    "next_page_token": {
      "type": "string",
      "description": "Token for fetching the next page of reviews"
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
| `search_parameters.num` | string |  |
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
    "id": "search_yawpDZvY5RcVxLm6PvWPdXoM",
    "status": "Success",
    "created_at": "2026-03-28T22:01:35Z",
    "request_time_taken": 2.09,
    "parsing_time_taken": 0.01,
    "total_time_taken": 2.1,
    "request_url": "https://play.google.com/store/apps/details?id=com.instagram.android&hl=en&gl=us",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_yawpDZvY5RcVxLm6PvWPdXoM.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_yawpDZ
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

- `apple_product_reviews`
- `scrape_review_platforms`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
