---
name: firecrawl_scrape_page_seo
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_scrape_page_seo`

Scrape a page with **combined HTML + structured SEO extraction** in one request.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `firecrawl`, `onpage`, `scrape`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_scrape_page_seo",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Full URL of the page to scrape (https is added automatically if missing). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Full URL of the page to scrape (https is added automatically if missing)."
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

Raw HTML, page metadata, and structured SEO extraction data

Key fields: `html`, `metadata`, `seo_data`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- PREFERRED tool for feeding data into seo_growth_audit and seo_growth_check_page
- Combines HTML + JSON extraction in ONE Firecrawl API call (costs ~2 requests due to extraction)
- Returns seo_data with LLM-extracted headings, links, images, paragraphs, schema, counts
- Pass $step.html to html_content and $step.seo_data to seo_data in seo_growth_audit
- Falls back to HTML-only if extraction fails — never degrades below firecrawl_scrape_page_html quality
- Auto-retries with stealth proxy on 401/403/500

**Chain groups:** `seo_growth`

## Alternatives

- `firecrawl_scrape_page_html`
- `firecrawl_scrape_website`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
