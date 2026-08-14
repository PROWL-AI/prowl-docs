---
name: ebay_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `ebay_search`

eBay Search — search products on eBay with prices and auction info.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "ebay_search",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Search query |
| `ebay_domain` | string | no |  | eBay domain |
| `page` | integer | no |  | Page number (for pagination) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "ebay_domain": {
      "type": "string",
      "description": "eBay domain"
    },
    "page": {
      "type": "integer",
      "description": "Page number (for pagination)",
      "minimum": 1
    }
  },
  "required": [
    "q"
  ]
}
```

## Example request

```json
{
  "q": "example query"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `categories`, `filters`, `organic_results`, `related_searches`

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
| `search_parameters.q` | string |  |
| `search_parameters.ebay_domain` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.delivery_country` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.sorted_by` | string |  |
| `search_information.buying_format` | string |  |
| `search_information.shipping_to` | string |  |
| `search_information.language` | string |  |
| `categories[]` | array<object> |  |
| `categories[].name` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_Lmagj14Ooqu7B8apR45E8MQp",
    "status": "Success",
    "created_at": "2026-03-28T20:44:05Z",
    "request_time_taken": 2.33,
    "parsing_time_taken": 0.06,
    "total_time_taken": 2.38,
    "request_url": "https://www.ebay.com/sch/i.html?_nkw=instagram.com&_fcid=1",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_Lmagj14Ooqu7B8apR45E8MQp.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_Lmagj14Ooqu7B8apR45E8MQp"

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

**Chain groups:** `searchapi_ecommerce`

## Alternatives

- `serpapi_ebay`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
