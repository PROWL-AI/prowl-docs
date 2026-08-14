---
name: serpapi_home_depot
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_home_depot`

Home Depot product search via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_home_depot",
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
| `country` | enum(us, ca) | no |  | Market — Home Depot serves only the US and Canada. Defaults to the run's market when one was stated. |
| `store_id` | string | no |  | Pin results to one US store; prices and stock are per store. |
| `delivery_zip` | string | no |  | Filter to products that ship to this postcode. |
| `sort` | enum(top_sellers, price_low_to_high, price_high_to_low, top_rated, best_match) | no |  | Sort order |

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
    "country": {
      "type": "string",
      "enum": [
        "us",
        "ca"
      ],
      "description": "Market \u2014 Home Depot serves only the US and Canada. Defaults to the run's market when one was stated."
    },
    "store_id": {
      "type": "string",
      "description": "Pin results to one US store; prices and stock are per store."
    },
    "delivery_zip": {
      "type": "string",
      "description": "Filter to products that ship to this postcode."
    },
    "sort": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "top_sellers",
        "price_low_to_high",
        "price_high_to_low",
        "top_rated",
        "best_match"
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
| `search_metadata.home_depot_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.q` | string |  |
| `search_parameters.nao` | string |  |
| `search_parameters.ps` | integer |  |
| `search_parameters.delivery_zip` | string |  |
| `search_parameters.store_id` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.engine` | string |  |
| `search_information` | object |  |
| `search_information.results_state` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.store_id` | string |  |
| `search_information.store_name` | string |  |
| `search_information.organic_results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d867dcfbef1176cd5de",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/mSi8Tbm-ec1qvFRm1roJaQ/69c83d867dcfbef1176cd5de.json",
    "created_at": "2026-03-28 20:43:50 UTC",
    "processed_at": "2026-03-28 20:43:50 UTC",
    "home_depot_url": "https://apionline.homedepot.com/b/N-5yc1v/Ntt-instagram.com?Nao=0",
    "raw_html_file": "https://serpapi.com/searches/mSi8Tbm-ec1qvFRm1roJaQ/69c83d867dcfbef1176cd5de.html",
    "prettify_htm
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

- `serpapi_amazon`
- `serpapi_apple_app_store`
- `serpapi_baidu`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
