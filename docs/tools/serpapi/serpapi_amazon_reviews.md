---
name: serpapi_amazon_reviews
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_amazon_reviews`

Amazon product reviews via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `amazon`, `reviews`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_amazon_reviews",
  "params": {
    "asin": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `asin` | string | yes |  | Amazon ASIN product identifier |
| `amazon_domain` | string | no |  | Amazon domain |
| `page` | integer | no |  | Page number for pagination |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "asin": {
      "type": "string",
      "description": "Amazon ASIN product identifier"
    },
    "amazon_domain": {
      "type": "string",
      "description": "Amazon domain"
    },
    "page": {
      "type": "integer",
      "description": "Page number for pagination",
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

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Unsupported `amazon_reviews` search engine."
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

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'serpapi_amazon', 'extract': '?'}`

## Alternatives

- `serpapi_amazon`
- `serpapi_amazon_product`
- `serpapi_apple_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
