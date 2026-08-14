---
name: serpapi_ebay_product
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_ebay_product`

eBay product details via SerpAPI.

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
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_ebay_product",
  "params": {
    "item_id": "item_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item_id` | string | yes |  | eBay item ID |
| `ebay_domain` | string | no |  | Regional eBay site the listing is read on, e.g. 'ebay.co.uk'. Changes price and currency. Defaults to ebay.com. |
| `locale` | string | no |  | Locale the search originates from. |
| `lang` | string | no |  | Language for the listing content. |
| `shipping_country` | string | no |  | Destination country used to calculate shipping cost and availability. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item_id": {
      "type": "string",
      "description": "eBay item ID"
    },
    "ebay_domain": {
      "type": "string",
      "description": "Regional eBay site the listing is read on, e.g. 'ebay.co.uk'. Changes price and currency. Defaults to ebay.com."
    },
    "locale": {
      "type": "string",
      "description": "Locale the search originates from."
    },
    "lang": {
      "type": "string",
      "description": "Language for the listing content."
    },
    "shipping_country": {
      "type": "string",
      "description": "Destination country used to calculate shipping cost and availability."
    }
  },
  "required": [
    "item_id"
  ]
}
```

## Example request

```json
{
  "item_id": "item_id_example"
}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Missing `product_id` query parameter."
}
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

**Chain inputs:** `{'param': 'item_id', 'from_tool': 'serpapi_ebay', 'extract': 'organic_results[].product_id'}`

**Chain groups:** `serpapi_ecommerce`

## Alternatives

- `ebay_product`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
