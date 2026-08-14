---
name: gemini_keyword_report
provider: Google Gemini
provider_slug: gemini
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `gemini_keyword_report`

Create a semantic keyword analysis report using Gemini AI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Google Gemini |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ai`, `google-gemini`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "gemini_keyword_report",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | string[] | yes |  | List of keywords to analyze and cluster |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of keywords to analyze and cluster"
    }
  },
  "required": [
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": []
}
```

## Output

Semantic keyword analysis with clusters and insights

Key fields: `top_10_most_repeated_keywords`, `negative_keywords`, `long_tail_keywords`, `main_summary`, `niche_of_the_product`, `target_audience`, `search_terms`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing GEMINI_API_KEY | Cannot use AI analysis tools — report available data without AI synthesis |
| 429 | Rate limit / quota exceeded | Wait 60s and retry once; Gemini has generous free tier |
| 500 | Gemini internal error | Retry up to 3 times (built-in); if all fail, returns None |

## When to use

- Use after collecting keywords from multiple competitors to synthesize insights

## Alternatives

- `exa_keyword_search`
- `dataforseo_ai_keyword_volume`
- `dataforseo_labs_amazon_product_keyword_intersections`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://ai.google.dev/gemini-api/docs
