---
name: exa_similar_search
provider: Exa
provider_slug: exa
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `exa_similar_search`

Find websites similar to a given URL using Exa's similarity search.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Exa |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `exa`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "exa_similar_search",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | URL to find similar websites for (e.g. 'example.com') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "URL to find similar websites for (e.g. 'example.com')"
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

Similar websites with title, URL, and summary

Key fields: `[].title`, `[].url`, `[].summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing EXA_API_KEY | Skip Exa tools, use Perplexity or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |

## When to use

- Does not require keywords — uses the URL itself for similarity matching
- Excellent for competitor discovery when you only have a URL

## Alternatives

- `spyfu_get_combined_competitors`
- `dataforseo_labs_competitors_domain`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.exa.ai
