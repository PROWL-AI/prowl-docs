---
name: serpapi_ebay
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_ebay`

eBay product search via SerpAPI.

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
  "tool_name": "serpapi_ebay",
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
| `ebay_domain` | string | no |  | Regional eBay site, e.g. 'ebay.co.uk', 'ebay.de'. Defaults to ebay.com — set it or you are pricing the US marketplace. |
| `location_id` | string | no |  | Seller-location filter. eBay's OWN numeric id, not an ISO code (US=1, CA=2, GB=3, JP=104; full list at serpapi.com/ebay-location-options). |
| `delivery_zip` | string | no |  | ZIP/postal code — restricts to items that ship to that area. |
| `preferred_location` | enum(Domestic, Regional, Worldwide) | no |  | Preferred seller location. Pass the word; it is translated to eBay's ordinal on the wire (SerpApi documents the words but returns HTTP 400 for them). |

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
    "ebay_domain": {
      "type": "string",
      "description": "Regional eBay site, e.g. 'ebay.co.uk', 'ebay.de'. Defaults to ebay.com \u2014 set it or you are pricing the US marketplace."
    },
    "location_id": {
      "type": "string",
      "description": "Seller-location filter. eBay's OWN numeric id, not an ISO code (US=1, CA=2, GB=3, JP=104; full list at serpapi.com/ebay-location-options)."
    },
    "delivery_zip": {
      "type": "string",
      "description": "ZIP/postal code \u2014 restricts to items that ship to that area."
    },
    "preferred_location": {
      "type": "string",
      "description": "Preferred seller location. Pass the word; it is translated to eBay's ordinal on the wire (SerpApi documents the words but returns HTTP 400 for them).",
      "enum": [
        "Domestic",
        "Regional",
        "Worldwide"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `categories`, `organic_results`, `related_searches`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.ebay_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters._nkw` | string |  |
| `search_information` | object |  |
| `search_information.organic_results_state` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.query_displayed` | string |  |
| `categories[]` | array<object> |  |
| `categories[].id` | integer |  |
| `categories[].name` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].title` | string |  |
| `organic_results[].link` | string |  |
| `organic_results[].serpapi_link` | string |  |
| `organic_results[].product_id` | string |  |
| `organic_results[].price` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d859b762dc3fe16f7f6",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/cgjLsmVQP97MQuezmWbDRw/69c83d859b762dc3fe16f7f6.json",
    "created_at": "2026-03-28 20:43:49 UTC",
    "processed_at": "2026-03-28 20:43:49 UTC",
    "ebay_url": "https://www.ebay.com/sch/i.html?_nkw=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/cgjLsmVQP97MQuezmWbDRw/69c83d859b762dc3fe16f7f6.html",
    "total_time_taken": 1.61
  },
  "s
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

- `ebay_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
