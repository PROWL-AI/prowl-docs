---
name: resolve_app_store_ids
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `resolve_app_store_ids`

Resolve App Store IDs — search Apple App Store and Google Play using the brand name plus optional domain, company name, and alternate queries (deduped, multi-search).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "resolve_app_store_ids",
  "params": {
    "brand_name": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `brand_name` | string | yes |  | Brand or app name to search for |
| `domain` | string | no |  | Optional: site domain (e.g. esimplus.me) — adds queries like brand+domain and site:apps.apple.com |
| `company_name` | string | no |  | Optional: legal or display company name if different from brand |
| `alternate_queries` | string[] | no |  | Optional extra search strings (e.g. 'eSIM Plus', product nicknames) |
| `gl` | string | no | `us` | Country code (default 'us') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "brand_name": {
      "type": "string",
      "description": "Brand or app name to search for"
    },
    "domain": {
      "type": "string",
      "description": "Optional: site domain (e.g. esimplus.me) \u2014 adds queries like brand+domain and site:apps.apple.com"
    },
    "company_name": {
      "type": "string",
      "description": "Optional: legal or display company name if different from brand"
    },
    "alternate_queries": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Optional extra search strings (e.g. 'eSIM Plus', product nicknames)"
    },
    "gl": {
      "type": "string",
      "description": "Country code (default 'us')",
      "default": "us"
    }
  },
  "required": [
    "brand_name"
  ]
}
```

## Example request

```json
{
  "brand_name": "example"
}
```

## Output

Top-level keys: `apple_product_id`, `google_play_product_id`, `apple_app_url`, `google_play_app_url`

| Path | Type | Description |
|------|------|-------------|
| `apple_product_id` | null |  |
| `google_play_product_id` | string |  |
| `apple_app_url` | null |  |
| `google_play_app_url` | string |  |

### Example response (from profile)

```json
{
  "apple_product_id": null,
  "google_play_product_id": "com.instagram.android",
  "apple_app_url": null,
  "google_play_app_url": "https://play.google.com/store/apps/details?id=com.instagram.android"
}
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SEARCH_API_KEY | Skip SearchAPI tools — use Exa or Perplexity as alternatives for web search |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 422 | Invalid parameters | Check query and filter parameters match the expected format |

## When to use

- SearchAPI.io engine tool — set locale/geo params when available for market-correct results
- Use a prior search/list tool to obtain IDs before detail/reviews calls

- Pass domain and alternate_queries when the brand string alone fails (e.g. domain slug vs full App Store title)
- Runs several deduped queries and keeps the best fuzzy match per store

## Alternatives

_None listed._

## Provider docs

https://www.searchapi.io/docs
