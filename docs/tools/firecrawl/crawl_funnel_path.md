---
name: crawl_funnel_path
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `crawl_funnel_path`

Crawl a marketing funnel step-by-step starting from an ad landing page URL.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `firecrawl`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "crawl_funnel_path",
  "params": {
    "start_url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `start_url` | string | yes |  | Landing page URL to start the funnel crawl from (typically from an ad's landing_page_url) |
| `max_steps` | integer | no | `6` | Maximum number of funnel steps to follow |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "start_url": {
      "type": "string",
      "description": "Landing page URL to start the funnel crawl from (typically from an ad's landing_page_url)"
    },
    "max_steps": {
      "type": "integer",
      "description": "Maximum number of funnel steps to follow",
      "default": 6
    }
  },
  "required": [
    "start_url"
  ]
}
```

## Example request

```json
{
  "start_url": "https://example.com"
}
```

## Output

Structured funnel path with step-by-step page data

Key fields: `start_url`, `total_steps`, `blocked_by`, `steps[].url`, `steps[].page_title`, `steps[].screenshot_url`, `steps[].cta_text`, `steps[].page_type`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Use AFTER ad discovery — extract landing_page_url from top creatives, then crawl each funnel
- Costs 1-6 firecrawl scrapes per call (one per funnel step); budget accordingly
- Feeds MODULE 04 (Funnel Intelligence) with step-by-step conversion path analysis

## Alternatives

_None listed._

## Provider docs

https://docs.firecrawl.dev
