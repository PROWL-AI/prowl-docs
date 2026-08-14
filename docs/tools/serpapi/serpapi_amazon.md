---
name: serpapi_amazon
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_amazon`

Amazon product search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `amazon`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_amazon",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `language` | string | no |  | Language code, e.g. 'de'. |
| `delivery_zip` | string | no |  | Amazon delivery ZIP/postal code — sets the delivery market. |
| `shipping_location` | string | no |  | Amazon shipping country. |
| `device` | enum(desktop, tablet, mobile) | no |  | Device type. |
| `q` | string | yes |  | Search query |
| `page` | integer | no |  | Page number for pagination |
| `sort` | enum(price-asc-rank, price-desc-rank, review-rank, date-desc-rank, featured-rank) | no |  | Sort order |
| `amazon_domain` | string | no |  | Amazon domain (e.g. 'amazon.com', 'amazon.co.uk') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "language": {
      "type": "string",
      "description": "Language code, e.g. 'de'."
    },
    "delivery_zip": {
      "type": "string",
      "description": "Amazon delivery ZIP/postal code \u2014 sets the delivery market."
    },
    "shipping_location": {
      "type": "string",
      "description": "Amazon shipping country."
    },
    "device": {
      "type": "string",
      "description": "Device type.",
      "enum": [
        "desktop",
        "tablet",
        "mobile"
      ]
    },
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "page": {
      "type": "integer",
      "description": "Page number for pagination",
      "minimum": 1
    },
    "sort": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "price-asc-rank",
        "price-desc-rank",
        "review-rank",
        "date-desc-rank",
        "featured-rank"
      ]
    },
    "amazon_domain": {
      "type": "string",
      "description": "Amazon domain (e.g. 'amazon.com', 'amazon.co.uk')"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `organic_results`, `featured_products`, `categories`, `filters`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.amazon_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.k` | string |  |
| `search_parameters.amazon_domain` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `search_information.query_displayed` | string |  |
| `search_information.store` | string |  |
| `search_information.page` | integer |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].position` | integer |  |
| `organic_results[].asin` | string |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].link_clean` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d84b9dbc4a043b9328a",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/0UDgXD1q_P0BrZDUHHcSfg/69c83d84b9dbc4a043b9328a.json",
    "created_at": "2026-03-28 20:43:48 UTC",
    "processed_at": "2026-03-28 20:43:48 UTC",
    "amazon_url": "https://www.amazon.com/s?k=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/0UDgXD1q_P0BrZDUHHcSfg/69c83d84b9dbc4a043b9328a.html",
    "total_time_taken": 51.09
  },
  "search_p
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

## Alternatives

- `amazon_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
