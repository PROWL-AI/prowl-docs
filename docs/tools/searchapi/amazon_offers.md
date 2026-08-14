---
name: amazon_offers
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `amazon_offers`

Amazon Offers — all sellers and pricing for a product by ASIN.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `amazon`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "amazon_offers",
  "params": {
    "asin": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asin` | string | yes |  | ASIN |
| `amazon_domain` | string | no |  | Amazon domain |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "asin": {
      "type": "string",
      "description": "ASIN"
    },
    "amazon_domain": {
      "type": "string",
      "description": "Amazon domain"
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
    }
  },
  "required": [
    "asin"
  ]
}
```

## Example request

```json
{
  "asin": "B08N5WRWNW"
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
| `search_parameters.asin` | string |  |
| `search_parameters.amazon_domain` | string |  |
| `search_parameters.delivery_country` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_JoY68Me7qNsAjEBbmv0axRVb",
    "status": "Success",
    "created_at": "2026-03-28T20:44:04Z",
    "request_time_taken": 1.56,
    "parsing_time_taken": 0.0,
    "total_time_taken": 1.56,
    "request_url": "https://www.amazon.com/dp/B0DCCYZ1K2?aod=1",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_JoY68Me7qNsAjEBbmv0axRVb.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_JoY68Me7qNsAjEBbmv0axRVb"
  },
  "search_pa
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

## Alternatives

- `amazon_search`
- `dataforseo_merchant_amazon_products`
- `dataforseo_merchant_amazon_sellers`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
