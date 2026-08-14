---
name: seo_growth_audit
provider: SEO Growth
provider_slug: seo_growth
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `seo_growth_audit`

Run a 120-point SEO Growth + AI Retrieval + Pattern Detection audit across 20 sections.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SEO Growth |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `True` |
| Chain role | `dependent` |
| Tags | `seo`, `seo-growth` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "seo_growth_audit",
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
| `html_content` | string | yes |  | Raw HTML content of the page (from firecrawl_scrape_page_seo or firecrawl_scrape_page_html) |
| `page_url` | string | yes |  | Full URL of the page being audited |
| `sitemap_xml` | string | no |  | Optional: raw XML sitemap for structure and timezone analysis |
| `website_info_json` | string | no |  | Optional: JSON from gemini_analyze_website for enriched context |
| `trust_pages_status` | string | no |  | Optional: JSON mapping trust-page paths to HTTP codes, e.g. {"/about": 200} |
| `rss_feed_xml` | string | no |  | Optional: raw XML content of RSS/Atom feed for crawl sync analysis |
| `response_headers` | string | no |  | Optional: JSON of HTTP response headers, e.g. {"alt-svc": "h3=..."} |
| `redirect_map` | string | no |  | Optional: JSON mapping URLs to redirect status codes, e.g. {"/old": 301} |
| `page_status_codes` | string | no |  | Optional: JSON mapping all discovered URLs to HTTP status codes |
| `target_query` | string | no |  | Optional: target search query the page should rank for |
| `business_goal` | string | no |  | Optional: business goal for the page (e.g., 'generate leads', 'sell product') |
| `all_discovered_urls` | string | no |  | Optional: JSON array of all site URLs for crawl waste analysis |
| `gsc_queries` | string | no |  | Optional: JSON array of Google Search Console queries for question harvesting |
| `competitor_sitemaps` | string | no |  | Optional: JSON array of competitor sitemap XML strings for gap analysis |
| `redirect_chains` | string | no |  | Optional: JSON array of redirect chain arrays, each chain is [{url, status_code, type}, ...] |
| `sitemap_urls` | string | no |  | Optional: JSON array of all URLs found in the sitemap |
| `internal_link_targets` | string | no |  | Optional: JSON object mapping URLs to inbound internal link counts |
| `hero_image_metadata` | string | no |  | Optional: JSON object with hero image metadata for entity image checks. Fields: src, alt, width, height, file_size_bytes, format. Obtain from page scrape or image analysis. |
| `seo_data` | string | no |  | Optional: JSON object with pre-extracted SEO signals from firecrawl_scrape_page_seo. Enriches the HTML parser with LLM-extracted content (headings, links, images, structured data). Pass $step.seo_data from firecrawl_scrape_page_seo output. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "html_content": {
      "type": "string",
      "description": "Raw HTML content of the page (from firecrawl_scrape_page_seo or firecrawl_scrape_page_html)"
    },
    "page_url": {
      "type": "string",
      "description": "Full URL of the page being audited"
    },
    "sitemap_xml": {
      "type": "string",
      "description": "Optional: raw XML sitemap for structure and timezone analysis"
    },
    "website_info_json": {
      "type": "string",
      "description": "Optional: JSON from gemini_analyze_website for enriched context"
    },
    "trust_pages_status": {
      "type": "string",
      "description": "Optional: JSON mapping trust-page paths to HTTP codes, e.g. {\"/about\": 200}"
    },
    "rss_feed_xml": {
      "type": "string",
      "description": "Optional: raw XML content of RSS/Atom feed for crawl sync analysis"
    },
    "response_headers": {
      "type": "string",
      "description": "Optional: JSON of HTTP response headers, e.g. {\"alt-svc\": \"h3=...\"}"
    },
    "redirect_map": {
      "type": "string",
      "description": "Optional: JSON mapping URLs to redirect status codes, e.g. {\"/old\": 301}"
    },
    "page_status_codes": {
      "type": "string",
      "description": "Optional: JSON mapping all discovered URLs to HTTP status codes"
    },
    "target_query": {
      "type": "string",
      "description": "Optional: target search query the page should rank for"
    },
    "business_goal": {
      "type": "string",
      "description": "Optional: business goal for the page (e.g., 'generate leads', 'sell product')"
    },
    "all_discovered_urls": {
      "type": "string",
      "description": "Optional: JSON array of all site URLs for crawl waste analysis"
    },
    "gsc_queries": {
      "type": "string",
      "description": "Optional: JSON array of Google Search Console queries for question harvesting"
    },
    "competitor_sitemaps": {
      "type": "string",
      "description": "Optional: JSON array of competitor sitemap XML strings for gap analysis"
    },
    "redirect_chains": {
      "type": "string",
      "description": "Optional: JSON array of redirect chain arrays, each chain is [{url, status_code, type}, ...]"
    },
    "sitemap_urls": {
      "type": "string",
      "description": "Optional: JSON array of all URLs found in the sitemap"
    },
    "internal_link_targets": {
      "type": "string",
      "description": "Optional: JSON object mapping URLs to inbound internal link counts"
    },
    "hero_image_metadata": {
      "type": "string",
      "description": "Optional: JSON object with hero image metadata for entity image checks. Fields: src, alt, width, height, file_size_bytes, format. Obtain from page scrape or image analysis."
    },
    "seo_data": {
      "type": "string",
      "description": "Optional: JSON object with pre-extracted SEO signals from firecrawl_scrape_page_seo. Enriches the HTML parser with LLM-extracted content (headings, links, images, structured data). Pass $step.seo_data from firecrawl_scrape_page_seo output."
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

SEO Growth + AI Retrieval + Pattern Detection report with dimension scores, findings, and action plan

Key fields: `url`, `overall_score`, `crawl_efficiency_score`, `ai_retrieval_score`, `intent_fit_score`, `entity_trust_score`, `conversion_readiness_score`, `section_scores`, `findings`, `summary`, `top_priorities`, `quick_wins`, `critical_fixes`, `experiments`, `page_classification`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| parse_error | HTML content could not be parsed | Ensure the html_content is valid HTML from Firecrawl scrape |

## When to use

- 120-point audit across 20 sections with 5 dimension scores
- PREFERRED: use firecrawl_scrape_page_seo to get html + seo_data in one call, then pass both
- FALLBACK: use firecrawl_scrape_page_html for lightweight HTML-only scrape (no extraction cost)
- Returns critical_fixes, quick_wins, and experiments as prioritized action plan
- page_classification shows site_type, page_type, intent_type, funnel_stage
- Pattern Detection section (16 checks) detects grey/black hat techniques
- seo_data enriches content extraction with LLM-parsed headings, links, images, structured data

- PREFERRED: Use firecrawl_scrape_page_seo to get HTML + seo_data in one call, then pass both to seo_growth_audit(html_content=$step.html, seo_data=$step.seo_data)
- FALLBACK: Use firecrawl_scrape_page_html for lightweight HTML-only scrape (no LLM extraction cost)
- Requires raw HTML content — seo_data enriches with LLM-extracted headings, links, images, schema
- Combine with gemini_analyze_website output via website_info_json for richer business context
- Returns a 0-100 overall score with five dimension scores and detailed findings per section
- 120-point audit across 20 sections: Technical SEO, Architecture, On-Page, Content Quality, Internal Linking, E-E-A-T, AI Retrieval/GEO, Local SEO, UX, Agentic SEO, Vector Semantics, AI Content Hygiene, Entity Image, UGC, Business Intent, Crawl Waste, Growth Opportunities, Pattern Detection, and more
- Optional inputs include seo_data, hero_image_metadata, redirect_chains, sitemap_urls, internal_link_targets

**Chain inputs:** `{'param': 'html_content', 'from_tool': 'firecrawl_scrape_page_seo', 'extract': 'html'}`

**Chain groups:** `seo_growth`

## Alternatives

- `seo_growth_check_page`

_Full paths: [catalog index](../README.md)._
