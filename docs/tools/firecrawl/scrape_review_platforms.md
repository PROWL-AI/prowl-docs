---
name: scrape_review_platforms
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `scrape_review_platforms`

Scrape reviews from Trustpilot, G2, and Capterra for a brand.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `firecrawl`, `reviews`, `scrape`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "scrape_review_platforms",
  "params": {
    "brand_name": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `brand_name` | string | yes |  | Brand or product name to search reviews for |
| `domain` | string | no |  | Brand domain (e.g. 'acme.com'). Used for Trustpilot URL. If empty, derived from brand_name. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "brand_name": {
      "type": "string",
      "description": "Brand or product name to search reviews for"
    },
    "domain": {
      "type": "string",
      "description": "Brand domain (e.g. 'acme.com'). Used for Trustpilot URL. If empty, derived from brand_name.",
      "default": ""
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

Review content from Trustpilot, G2, and Capterra

Key fields: `trustpilot`, `g2`, `capterra`, `source_urls`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Use for Voice & Vulnerability module — replaces 3 separate firecrawl_search calls
- Costs 3-6 firecrawl requests (direct scrape + search fallback per platform)
- Combine output with app store reviews and pass to gemini_reviews_report

## Alternatives

- `google_maps`
- `google_forums`
- `dataforseo_biz_google_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
