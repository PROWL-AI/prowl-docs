---
name: exa_get_contents
provider: Exa
provider_slug: exa
category: web
generated_at: 2026-09-18T14:01:48Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `exa_get_contents`

Retrieve page contents for a list of URLs via Exa.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Exa |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `exa`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "exa_get_contents",
  "params": {
    "urls": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `urls` | string[] | yes |  | List of URLs to fetch content for |
| `text` | boolean | no | `True` | Include full text content |
| `summary` | boolean | no | `False` | Include AI-generated summary |
| `highlights` | boolean | no | `False` | Include key highlights |
| `livecrawl` | enum(always, fallback, never, auto, preferred) | no |  | Freshness policy. Exa serves its cached copy unless this says otherwise: 'always' crawls now, 'preferred' tries and falls back, 'fallback' crawls only when nothing is cached, 'never' uses the cache alone, 'auto' lets Exa decide. Use 'always' for pricing or changelog pages where a stale snapshot is wrong. |
| `livecrawl_timeout` | integer | no |  | Milliseconds to wait for a live crawl before falling back. |
| `max_age_hours` | integer | no |  | Reject a cached copy older than this many hours. |
| `subpages` | integer | no |  | Also fetch up to N subpages of each URL. |
| `subpage_target` | string | no |  | Restrict those subpages to a path, e.g. 'pricing'. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "urls": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of URLs to fetch content for"
    },
    "text": {
      "type": "boolean",
      "description": "Include full text content",
      "default": true
    },
    "summary": {
      "type": "boolean",
      "description": "Include AI-generated summary",
      "default": false
    },
    "highlights": {
      "type": "boolean",
      "description": "Include key highlights",
      "default": false
    },
    "livecrawl": {
      "type": "string",
      "description": "Freshness policy. Exa serves its cached copy unless this says otherwise: 'always' crawls now, 'preferred' tries and falls back, 'fallback' crawls only when nothing is cached, 'never' uses the cache alone, 'auto' lets Exa decide. Use 'always' for pricing or changelog pages where a stale snapshot is wrong.",
      "enum": [
        "always",
        "fallback",
        "never",
        "auto",
        "preferred"
      ]
    },
    "livecrawl_timeout": {
      "type": "integer",
      "description": "Milliseconds to wait for a live crawl before falling back.",
      "minimum": 1
    },
    "max_age_hours": {
      "type": "integer",
      "description": "Reject a cached copy older than this many hours.",
      "minimum": 1
    },
    "subpages": {
      "type": "integer",
      "description": "Also fetch up to N subpages of each URL.",
      "minimum": 1
    },
    "subpage_target": {
      "type": "string",
      "description": "Restrict those subpages to a path, e.g. 'pricing'."
    }
  },
  "required": [
    "urls"
  ]
}
```

## Example request

```json
{
  "urls": "https://example.com"
}
```

## Output

Page contents for each URL with text, summary, and highlights. A page fetched with `subpages` carries them under `[].subpages`, shaped the same way; the key is absent when there are none.

Key fields: `[].url`, `[].text`, `[].summary`, `[].highlights`, `[].subpages`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing EXA_API_KEY | Skip Exa tools, use Perplexity or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |

## When to use

- Use when you already have URLs and need their content — avoids redundant searches
- Enable summary=True for concise AI-generated summaries of each page

## Alternatives

- `firecrawl_scrape_website`
- `firecrawl_scrape_page_markdown`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.exa.ai
