---
name: firecrawl_search
provider: Firecrawl
provider_slug: firecrawl
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `firecrawl_search`

Search the web for information using Firecrawl search.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Firecrawl |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `firecrawl`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "firecrawl_search",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `country` | string | no |  | ISO country for the search. Defaults to the run's market; Firecrawl itself defaults to US. |
| `tbs` | string | no |  | Freshness filter: qdr:h/d/w/m/y, or cdr with cd_min/cd_max dates. |
| `sources` | any[] | no |  | Which corpora to search: web, images, news. |
| `categories` | any[] | no |  | Restrict to github, research or pdf. |
| `include_domains` | any[] | no |  | Only return results from these hostnames. |
| `exclude_domains` | any[] | no |  | Never return results from these hostnames. |
| `query` | string | yes |  | Search query (e.g. 'Product information for example.com') |
| `limit` | integer | no | `10` | Maximum number of results to return |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "country": {
      "type": "string",
      "description": "ISO country for the search. Defaults to the run's market; Firecrawl itself defaults to US."
    },
    "tbs": {
      "type": "string",
      "description": "Freshness filter: qdr:h/d/w/m/y, or cdr with cd_min/cd_max dates."
    },
    "sources": {
      "type": "array",
      "description": "Which corpora to search: web, images, news."
    },
    "categories": {
      "type": "array",
      "description": "Restrict to github, research or pdf."
    },
    "include_domains": {
      "type": "array",
      "description": "Only return results from these hostnames."
    },
    "exclude_domains": {
      "type": "array",
      "description": "Never return results from these hostnames."
    },
    "query": {
      "type": "string",
      "description": "Search query (e.g. 'Product information for example.com')"
    },
    "limit": {
      "type": "integer",
      "description": "Maximum number of results to return",
      "default": 10
    }
  },
  "required": [
    "query"
  ]
}
```

## Example request

```json
{
  "query": "example query"
}
```

## Output

Scraped web documents with markdown content

Key fields: `[].url`, `[].markdown`, `[].metadata`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FIRECRAWL_API_KEY | Skip Firecrawl tools, use alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 408 | Scrape timeout — target page too slow | Retry once; if still fails, try firecrawl_scrape_page_markdown (lighter) |

## When to use

- Review analysis workflow: use query '{domain} reviews' to find reviews
- Follow up with gemini_reviews_report for sentiment analysis of the found reviews

## Alternatives

- `perplexity_search`
- `perplexity_search_by_query`
- `exa_keyword_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.firecrawl.dev
