---
name: exa_keyword_search
provider: Exa
provider_slug: exa
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `exa_keyword_search`

Search for competitor products and similar services using Exa AI-powered search.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Exa |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `exa`, `keywords`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "exa_keyword_search",
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
| `num_results` | integer | no |  | Results to return (1-100). |
| `type` | enum(instant, fast, auto, deep-lite, deep, deep-reasoning) | no |  | Search strategy. |
| `category` | enum(company, publication, news, personal site, financial report, people) | no |  | Restrict to a document class. |
| `include_domains` | any[] | no |  | Only return results from these domains. |
| `exclude_domains` | any[] | no |  | Additional domains to exclude (the researched domain is always excluded). |
| `start_published_date` | string | no |  | Only documents published on or after this ISO 8601 date. |
| `end_published_date` | string | no |  | Only documents published on or before this ISO 8601 date. |
| `include_text` | any[] | no |  | Require these strings to appear in the result text. |
| `exclude_text` | any[] | no |  | Reject results containing these strings. |
| `user_location` | string | no |  | Two-letter ISO country for result relevance. Defaults to the run's market. |
| `url` | string | yes |  | Target domain URL to exclude from results |
| `product_name` | string | yes |  | Name of the target product |
| `keywords` | string[] | yes |  | List of keywords related to the product |
| `search_query` | string[] | no |  | List of search terms to find relevant products |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "num_results": {
      "type": "integer",
      "description": "Results to return (1-100).",
      "minimum": 1,
      "maximum": 100
    },
    "type": {
      "type": "string",
      "description": "Search strategy.",
      "enum": [
        "instant",
        "fast",
        "auto",
        "deep-lite",
        "deep",
        "deep-reasoning"
      ]
    },
    "category": {
      "type": "string",
      "description": "Restrict to a document class.",
      "enum": [
        "company",
        "publication",
        "news",
        "personal site",
        "financial report",
        "people"
      ]
    },
    "include_domains": {
      "type": "array",
      "description": "Only return results from these domains."
    },
    "exclude_domains": {
      "type": "array",
      "description": "Additional domains to exclude (the researched domain is always excluded)."
    },
    "start_published_date": {
      "type": "string",
      "description": "Only documents published on or after this ISO 8601 date."
    },
    "end_published_date": {
      "type": "string",
      "description": "Only documents published on or before this ISO 8601 date."
    },
    "include_text": {
      "type": "array",
      "description": "Require these strings to appear in the result text."
    },
    "exclude_text": {
      "type": "array",
      "description": "Reject results containing these strings."
    },
    "user_location": {
      "type": "string",
      "description": "Two-letter ISO country for result relevance. Defaults to the run's market."
    },
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
      "description": "List of search terms to find relevant products"
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

List of competitor products with title, URL, and summary

Key fields: `[].title`, `[].url`, `[].summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing EXA_API_KEY | Skip Exa tools, use Perplexity or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |

## When to use

- Best when you already know the product's keywords — uses keyword matching
- Combine with exa_similar_search for broader competitor discovery

## Alternatives

- `google_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.exa.ai
