---
name: serpapi_walmart
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_walmart`

Walmart product search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_walmart",
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
| `page` | integer | no |  | Page number for pagination |
| `sort` | enum(best_seller, best_match, price_low, price_high, rating_high, new) | no |  | Sort order |
| `store_id` | string | no |  | Walmart store identifier for local availability. |
| `walmart_domain` | enum(walmart.com, walmart.com.mx) | no |  | Walmart marketplace domain. |
| `min_price` | number | no |  | Minimum price filter. |
| `max_price` | number | no |  | Maximum price filter. |
| `device` | enum(desktop, tablet, mobile) | no |  | Device type. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
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
        "best_seller",
        "best_match",
        "price_low",
        "price_high",
        "rating_high",
        "new"
      ]
    },
    "store_id": {
      "type": "string",
      "description": "Walmart store identifier for local availability."
    },
    "walmart_domain": {
      "type": "string",
      "description": "Walmart marketplace domain.",
      "enum": [
        "walmart.com",
        "walmart.com.mx"
      ]
    },
    "min_price": {
      "type": "number",
      "description": "Minimum price filter."
    },
    "max_price": {
      "type": "number",
      "description": "Maximum price filter."
    },
    "device": {
      "type": "string",
      "description": "Device type.",
      "enum": [
        "desktop",
        "tablet",
        "mobile"
      ]
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `error`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.walmart_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.device` | string |  |
| `search_parameters.query` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d85f0114aaf666ec8a2",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/vTbtFpG6AzjIGJSYmWx7Kg/69c83d85f0114aaf666ec8a2.json",
    "created_at": "2026-03-28 20:43:49 UTC",
    "processed_at": "2026-03-28 20:43:49 UTC",
    "walmart_url": "https://www.walmart.com/search?query=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/vTbtFpG6AzjIGJSYmWx7Kg/69c83d85f0114aaf666ec8a2.html",
    "prettify_html_file": "https://
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

**Chain groups:** `serpapi_ecommerce`

## Alternatives

- `walmart_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
