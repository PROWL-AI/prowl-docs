---
name: perplexity_search
provider: Perplexity
provider_slug: perplexity
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `perplexity_search`

AI-powered web search via Perplexity to find competitor products and services.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Perplexity |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `perplexity`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "perplexity_search",
  "params": {
    "keywords": [],
    "product_name": "example",
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Target domain URL to exclude from results |
| `product_name` | string | yes |  | Name of the target product |
| `keywords` | string[] | yes |  | List of keywords related to the product |
| `search_query` | string[] | no |  | List of search queries to find relevant products |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Target domain URL to exclude from results"
    },
    "product_name": {
      "type": "string",
      "description": "Name of the target product"
    },
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of keywords related to the product"
    },
    "search_query": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of search queries to find relevant products"
    }
  },
  "required": [
    "url",
    "product_name",
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": [],
  "product_name": "example",
  "url": "https://example.com"
}
```

## Output

Competitor products with title, URL, snippet

Key fields: `[].title`, `[].url`, `[].summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing PERPLEXITY_API_KEY | Skip Perplexity tools, use Exa or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 60s and retry once |

## When to use

- Complementary to exa_keyword_search — use both for broader coverage

## Alternatives

- `firecrawl_search`
- `exa_keyword_search`
- `exa_similar_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.perplexity.ai/api-reference
