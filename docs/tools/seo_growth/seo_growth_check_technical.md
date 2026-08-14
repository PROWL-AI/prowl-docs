---
name: seo_growth_check_technical
provider: SEO Growth
provider_slug: seo_growth
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `seo_growth_check_technical`

Site-wide technical SEO + pattern detection check: trust pages, sitemap, mass 404s, redirect chain analysis, TLS/HTTP3, CDN detection, RSS+sitemap sync, plus search page indexab...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SEO Growth |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `True` |
| Chain role | `standalone` |
| Tags | `seo`, `seo-growth` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "seo_growth_check_technical",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `sitemap_xml` | string | no |  | Raw XML content of the site's sitemap.xml |
| `trust_pages_status` | string | no |  | JSON mapping trust-page paths to HTTP status codes |
| `rss_feed_xml` | string | no |  | Optional: raw XML content of RSS/Atom feed |
| `response_headers` | string | no |  | Optional: JSON of HTTP response headers |
| `redirect_map` | string | no |  | Optional: JSON mapping URLs to redirect status codes |
| `page_status_codes` | string | no |  | Optional: JSON mapping all URLs to HTTP status codes |
| `redirect_chains` | string | no |  | Optional: JSON array of redirect chain arrays for chain analysis |
| `all_discovered_urls` | string | no |  | Optional: JSON array of all site URLs for pattern detection |
| `sitemap_urls` | string | no |  | Optional: JSON array of all URLs found in the sitemap |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "sitemap_xml": {
      "type": "string",
      "description": "Raw XML content of the site's sitemap.xml"
    },
    "trust_pages_status": {
      "type": "string",
      "description": "JSON mapping trust-page paths to HTTP status codes"
    },
    "rss_feed_xml": {
      "type": "string",
      "description": "Optional: raw XML content of RSS/Atom feed"
    },
    "response_headers": {
      "type": "string",
      "description": "Optional: JSON of HTTP response headers"
    },
    "redirect_map": {
      "type": "string",
      "description": "Optional: JSON mapping URLs to redirect status codes"
    },
    "page_status_codes": {
      "type": "string",
      "description": "Optional: JSON mapping all URLs to HTTP status codes"
    },
    "redirect_chains": {
      "type": "string",
      "description": "Optional: JSON array of redirect chain arrays for chain analysis"
    },
    "all_discovered_urls": {
      "type": "string",
      "description": "Optional: JSON array of all site URLs for pattern detection"
    },
    "sitemap_urls": {
      "type": "string",
      "description": "Optional: JSON array of all URLs found in the sitemap"
    }
  },
  "required": []
}
```

## Example request

```json
{}
```

## Output

Top-level keys: `overall_score`, `section_scores`, `findings`, `top_priorities`

| Path | Type | Description |
|------|------|-------------|
| `overall_score` | integer |  |
| `section_scores` | object |  |
| `section_scores.Technical SEO` | integer |  |
| `findings[]` | array<object> |  |
| `findings[].check_id` | string |  |
| `findings[].section` | string |  |
| `findings[].title` | string |  |
| `findings[].status` | string |  |
| `findings[].severity` | string |  |
| `findings[].details` | string |  |
| `findings[].recommendation` | string |  |
| `findings[].growth_hack` | string |  |
| `top_priorities[]` | array<string> |  |

### Example response (from profile)

```json
{
  "overall_score": 0,
  "section_scores": {
    "Technical SEO": 0
  },
  "findings": [
    {
      "check_id": "tech_trust_pages",
      "section": "Technical SEO",
      "title": "Trust & Spam-Signal Pages",
      "status": "fail",
      "severity": "high",
      "details": "Missing trust pages: /privacy-policy, /privacy, /legal/privacy, /about, /about-us, /terms, /terms-of-service, /tos, /contact, /contact-us, /ads.txt, /favicon.ico. Found: none.",
      "recommendation": "Create the follow
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| parse_error | HTML content could not be parsed | Ensure the html_content is valid HTML from Firecrawl scrape |

## When to use

- Technical health check without page HTML — covers server-side signals
- New: mass 404 detection, redirect chain analysis, HTTP/3, CDN, RSS sync

- Use for site-wide technical SEO health check without page HTML
- Provide sitemap XML and/or trust-page status codes for best results

## Alternatives

_None listed._
