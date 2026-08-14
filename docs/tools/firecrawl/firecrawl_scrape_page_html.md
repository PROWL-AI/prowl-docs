---
name: firecrawl_scrape_page_html
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_scrape_page_html`

Scrape a single page and return its **raw HTML** plus metadata.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `firecrawl`, `onpage`, `scrape`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_scrape_page_html",
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

Raw HTML string and page metadata

Key fields: `html`, `metadata`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Lightweight HTML-only scrape — use when structured extraction is not needed or budget is tight
- Costs 1 firecrawl request; auto-retries with stealth proxy on 401/403/500
- Returns only_main_content=False so SEO audits see the full DOM including nav, footer, ads
- For enriched SEO audit, prefer firecrawl_scrape_page_seo instead

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'google_search', 'extract': '?'}`

## Alternatives

- `firecrawl_scrape_page_seo`
- `firecrawl_scrape_website`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
