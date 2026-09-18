---
name: firecrawl_map_domain
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-09-18T14:59:05Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_map_domain`

Map a domain's sitemap to discover all pages with their titles and descriptions.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `domain`, `firecrawl`, `maps`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_map_domain",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Domain URL to map (e.g. 'example.com') |
| `limit` | integer | no | `10` | Maximum number of pages to return |
| `search` | string | no |  | Only return pages matching this term, e.g. 'pricing'. |
| `include_subdomains` | boolean | no |  | Also map pages on subdomains of this domain. |
| `sitemap` | enum(only, include, skip) | no |  | How the sitemap is used: 'include' (default) maps from the sitemap and discovery, 'only' trusts the sitemap alone, 'skip' ignores it — the mode for a site that has no sitemap. |
| `timeout` | integer | no |  | Milliseconds to allow the map before giving up. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Domain URL to map (e.g. 'example.com')"
    },
    "limit": {
      "type": "integer",
      "description": "Maximum number of pages to return",
      "default": 10
    },
    "search": {
      "type": "string",
      "description": "Only return pages matching this term, e.g. 'pricing'."
    },
    "include_subdomains": {
      "type": "boolean",
      "description": "Also map pages on subdomains of this domain."
    },
    "sitemap": {
      "type": "string",
      "description": "How the sitemap is used: 'include' (default) maps from the sitemap and discovery, 'only' trusts the sitemap alone, 'skip' ignores it \u2014 the mode for a site that has no sitemap.",
      "enum": [
        "only",
        "include",
        "skip"
      ]
    },
    "timeout": {
      "type": "integer",
      "description": "Milliseconds to allow the map before giving up.",
      "minimum": 1
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

List of pages with URL, title, and description

Key fields: `[].url`, `[].title`, `[].description`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Use to understand website structure before deeper scraping

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'find_subdomains', 'extract': '?'}`

## Alternatives

- `dataforseo_serp_google_maps`
- `extract_domain_from_url`
- `find_subdomains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
