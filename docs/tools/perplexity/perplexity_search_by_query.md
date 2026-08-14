---
name: perplexity_search_by_query
provider: Perplexity
provider_slug: perplexity
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `perplexity_search_by_query`

Search for products and services using a single specific query via Perplexity.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Perplexity |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `perplexity`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "perplexity_search_by_query",
  "params": {
    "search_query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `search_query` | string | yes |  | The search query string |
| `ignore_domain` | string | no |  | Domain to exclude from results (optional) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "search_query": {
      "type": "string",
      "description": "The search query string"
    },
    "ignore_domain": {
      "type": "string",
      "description": "Domain to exclude from results (optional)"
    }
  },
  "required": [
    "search_query"
  ]
}
```

## Example request

```json
{
  "search_query": "example query"
}
```

## Output

Search results with title, URL, snippet

Key fields: `[].title`, `[].url`, `[].summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing PERPLEXITY_API_KEY | Skip Perplexity tools, use Exa or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 60s and retry once |

## When to use

- Simpler than perplexity_search — pass a single query string for targeted searches

**Chain groups:** `gemini`

## Alternatives

- `firecrawl_search`
- `exa_keyword_search`
- `exa_similar_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.perplexity.ai/api-reference
