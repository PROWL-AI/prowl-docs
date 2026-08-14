---
name: firecrawl_scrape_website
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_scrape_website`

Scrape a website URL to extract structured product data (name, description, features, pricing, CTAs, navigation URLs, social links, contact info) plus markdown content of the ho...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `firecrawl`, `scrape`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_scrape_website",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Full URL or domain to scrape (e.g. 'https://example.com' or 'example.com') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Full URL or domain to scrape (e.g. 'https://example.com' or 'example.com')"
    }
  },
  "required": [
    "url"
  ]
}
```

## Example request

```json
{
  "url": "https://example.com"
}
```

## Output

Structured product data + markdown of homepage and navigation pages

Key fields: `product_name`, `product_description`, `features`, `pricing`, `ctas`, `navigation_urls`, `social_links`, `contact_info`, `pages_data`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Use as the FIRST step when analyzing any website or domain
- Heavy — homepage JSON scrape (capped) + up to 7 nav pages under a ~100s budget; use firecrawl_scrape_page_markdown for lighter scrapes

- Heavy — homepage scrape (time-capped) + up to 7 navigation pages under ~100s total budget; use firecrawl_scrape_page_markdown for lighter scrapes

**Chain groups:** `gemini`

## Alternatives

- `firecrawl_scrape_page_markdown`
- `exa_get_contents`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
