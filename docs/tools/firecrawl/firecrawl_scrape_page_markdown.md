---
name: firecrawl_scrape_page_markdown
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_scrape_page_markdown`

Scrape a single web page and return its content as markdown.

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
  "tool_name": "firecrawl_scrape_page_markdown",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `country` | string | no |  | ISO 3166-1 alpha-2 exit country for the fetch. Defaults to the run's market; Firecrawl itself defaults to US. |
| `languages` | any[] | no |  | Accept-Language preferences for the fetch. |
| `mobile` | boolean | no |  | Emulate a mobile device. |
| `wait_for` | integer | no |  | Milliseconds to wait before capturing, for JS-rendered pages. |
| `only_main_content` | boolean | no |  | Strip headers, navs and footers (default true). |
| `include_tags` | any[] | no |  | Only keep these HTML tags/selectors. |
| `exclude_tags` | any[] | no |  | Drop these HTML tags/selectors. |
| `timeout` | integer | no |  | Request timeout in milliseconds (1000-300000). |
| `max_age` | integer | no |  | Serve a cached copy younger than this many milliseconds. |
| `block_ads` | boolean | no |  | Block ads and cookie banners (default true). |
| `url` | string | yes |  | URL of the page to scrape |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "country": {
      "type": "string",
      "description": "ISO 3166-1 alpha-2 exit country for the fetch. Defaults to the run's market; Firecrawl itself defaults to US."
    },
    "languages": {
      "type": "array",
      "description": "Accept-Language preferences for the fetch."
    },
    "mobile": {
      "type": "boolean",
      "description": "Emulate a mobile device."
    },
    "wait_for": {
      "type": "integer",
      "description": "Milliseconds to wait before capturing, for JS-rendered pages."
    },
    "only_main_content": {
      "type": "boolean",
      "description": "Strip headers, navs and footers (default true)."
    },
    "include_tags": {
      "type": "array",
      "description": "Only keep these HTML tags/selectors."
    },
    "exclude_tags": {
      "type": "array",
      "description": "Drop these HTML tags/selectors."
    },
    "timeout": {
      "type": "integer",
      "description": "Request timeout in milliseconds (1000-300000)."
    },
    "max_age": {
      "type": "integer",
      "description": "Serve a cached copy younger than this many milliseconds."
    },
    "block_ads": {
      "type": "boolean",
      "description": "Block ads and cookie banners (default true)."
    },
    "url": {
      "type": "string",
      "description": "URL of the page to scrape"
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

Page content as markdown text

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Cheaper and faster than firecrawl_scrape_website — use for individual pages

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'google_search', 'extract': '?'}`

## Alternatives

- `firecrawl_scrape_website`
- `exa_get_contents`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
