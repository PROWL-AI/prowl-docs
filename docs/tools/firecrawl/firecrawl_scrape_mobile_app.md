---
name: firecrawl_scrape_mobile_app
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_scrape_mobile_app`

Scrape an App Store or Google Play page (and Sensor Tower if available) to extract mobile app data: name, description, downloads, revenue, ratings, version, publisher.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `firecrawl`, `scrape`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_scrape_mobile_app",
  "params": {
    "app_page_url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `app_page_url` | string | yes |  | App Store or Google Play URL (e.g. 'https://apps.apple.com/app/idXXXXX') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "app_page_url": {
      "type": "string",
      "description": "App Store or Google Play URL (e.g. 'https://apps.apple.com/app/idXXXXX')"
    }
  },
  "required": [
    "app_page_url"
  ]
}
```

## Example request

```json
{
  "app_page_url": "https://example.com"
}
```

## Output

Mobile app data (MobileAppInfo records): app name, description, monthly downloads/revenue, content rating

Key fields: `[].app_name`, `[].description`, `[].monthly_downloads`, `[].monthly_revenue`, `[].content_rating`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Also scrapes Sensor Tower data when available for richer app intelligence

## Alternatives

- `firecrawl_scrape_page_seo`
- `firecrawl_scrape_website`
- `scrape_review_platforms`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
