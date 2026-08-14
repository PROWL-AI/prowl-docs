---
name: exa_answer
provider: Exa
provider_slug: exa
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `exa_answer`

AI-powered Q&A via Exa Answer API.

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
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "exa_answer",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | The question to answer |
| `text` | boolean | no | `True` | Include source text in citations |
| `model` | string | no |  | Optional model override (e.g. 'exa-lite') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "The question to answer"
    },
    "text": {
      "type": "boolean",
      "description": "Include source text in citations",
      "default": true
    },
    "model": {
      "type": "string",
      "description": "Optional model override (e.g. 'exa-lite')"
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

AI-generated answer with web citations

Key fields: `answer`, `citations[].url`, `citations[].text`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing EXA_API_KEY | Skip Exa tools, use Perplexity or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |

## When to use

- More focused than general search — ideal for factual questions with definitive answers

## Alternatives

_None listed._

## Provider docs

https://docs.exa.ai
