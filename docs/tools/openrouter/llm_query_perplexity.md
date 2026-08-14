---
name: llm_query_perplexity
provider: OpenRouter
provider_slug: openrouter
category: ai
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `llm_query_perplexity`

Ask Perplexity sonar (web-grounded) about a brand, keyword, product, or concept.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | OpenRouter |
| Category | `ai` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ai`, `openrouter` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "llm_query_perplexity",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | The question to ask the model. Phrase as a direct question (e.g. 'What do you know about Notion as a product?') so the model returns its trained knowledge. |
| `system_prompt` | string | no |  | Optional system prompt override. Defaults to a factual knowledge-style instruction. Use to shape tone (e.g. 'Respond in 3 bullet points'). |
| `max_tokens` | integer | no | `2000` | Max output tokens. |
| `temperature` | number | no | `0.2` | Sampling temperature (0.0-1.0). Lower = more factual. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "The question to ask the model. Phrase as a direct question (e.g. 'What do you know about Notion as a product?') so the model returns its trained knowledge."
    },
    "system_prompt": {
      "type": "string",
      "description": "Optional system prompt override. Defaults to a factual knowledge-style instruction. Use to shape tone (e.g. 'Respond in 3 bullet points')."
    },
    "max_tokens": {
      "type": "integer",
      "description": "Max output tokens.",
      "default": 2000
    },
    "temperature": {
      "type": "number",
      "description": "Sampling temperature (0.0-1.0). Lower = more factual.",
      "default": 0.2
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

LLM response with token usage, cost, and (where available) citations.

Key fields: `provider`, `model`, `response_text`, `input_tokens`, `output_tokens`, `cost_usd`, `citations[].url`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing OPENROUTER_API_KEY | Skip llm_query_* tools or fix the key. |
| 429 | OpenRouter or upstream provider rate limit | Retry with backoff; consider switching provider. |
| 502 | Upstream model timeout / unavailable | Try another llm_query_* tool with a different model family. |

## When to use

- Pick this when you want citations / source URLs alongside the model's answer.
- Use alongside llm_query_openai / _anthropic / _gemini / _grok for a 'what does each model think?' comparison.

## Alternatives

_None listed._

## Provider docs

https://openrouter.ai/docs
