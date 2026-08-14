---
name: seo_growth_check_page
provider: SEO Growth
provider_slug: seo_growth
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `seo_growth_check_page`

Lightweight single-page SEO check covering architecture, on-page, content quality, vector semantics, AI content hygiene, and page-level pattern detection (canonical abuse, DOM e...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SEO Growth |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `True` |
| Chain role | `dependent` |
| Tags | `onpage`, `seo`, `seo-growth` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "seo_growth_check_page",
  "params": {
    "html_content": "example",
    "page_url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `html_content` | string | yes |  | Raw HTML content of the page |
| `page_url` | string | yes |  | Full URL of the page being checked |
| `seo_data` | string | no |  | Optional: JSON with pre-extracted SEO signals from firecrawl_scrape_page_seo |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "html_content": {
      "type": "string",
      "description": "Raw HTML content of the page"
    },
    "page_url": {
      "type": "string",
      "description": "Full URL of the page being checked"
    },
    "seo_data": {
      "type": "string",
      "description": "Optional: JSON with pre-extracted SEO signals from firecrawl_scrape_page_seo"
    }
  },
  "required": [
    "html_content",
    "page_url"
  ]
}
```

## Example request

```json
{
  "html_content": "example",
  "page_url": "https://example.com"
}
```

## Output

Top-level keys: `url`, `overall_score`, `section_scores`, `findings`, `top_priorities`

| Path | Type | Description |
|------|------|-------------|
| `url` | string |  |
| `overall_score` | integer |  |
| `section_scores` | object |  |
| `section_scores.On-Page` | integer |  |
| `findings[]` | array<object> |  |
| `findings[].check_id` | string |  |
| `findings[].section` | string |  |
| `findings[].title` | string |  |
| `findings[].status` | string |  |
| `findings[].severity` | string |  |
| `findings[].details` | string |  |
| `findings[].recommendation` | string |  |
| `findings[].growth_hack` | null |  |
| `top_priorities[]` | array<string> |  |

### Example response (from profile)

```json
{
  "url": "https://www.nike.com",
  "overall_score": 9,
  "section_scores": {
    "On-Page": 9
  },
  "findings": [
    {
      "check_id": "onpage_title_length",
      "section": "On-Page",
      "title": "Title Tag Length Exploitation",
      "status": "fail",
      "severity": "critical",
      "details": "No <title> tag found on the page.",
      "recommendation": "Add a title tag immediately — this is the single most important on-page ranking factor.",
      "growth_hack": null
    },
    
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| parse_error | HTML content could not be parsed | Ensure the html_content is valid HTML from Firecrawl scrape |

## When to use

- Quick per-page check with content quality, vector semantics, and AI hygiene
- Returns page_classification alongside findings

- Use for quick per-page checks when full audit is not needed
- Covers URL structure, title/H1 optimization, content quality, and internal linking

**Chain inputs:** `{'param': 'html_content', 'from_tool': 'firecrawl_scrape_page_seo', 'extract': 'html'}`

**Chain groups:** `seo_growth`

## Alternatives

- `seo_growth_audit`

_Full paths: [catalog index](../README.md)._
