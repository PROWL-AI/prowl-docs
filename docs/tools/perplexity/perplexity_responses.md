---
name: perplexity_responses
provider: Perplexity
provider_slug: perplexity
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `perplexity_responses`

Agentic pro-search via Perplexity Responses API.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Perplexity |
| Category | `web` |
| Timeout | 180 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `perplexity`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "perplexity_responses",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | The question or research task |
| `preset` | string | no | `pro-search` | Preset to use (default 'pro-search') |
| `model` | string | no |  | Override the model the preset would pick |
| `instructions` | string | no |  | System-level instructions for the agent |
| `language_preference` | string | no |  | Preferred answer language, e.g. 'de' |
| `max_output_tokens` | integer | no |  | Cap the answer length |
| `max_steps` | integer | no |  | Cap how many research steps the agent may take |
| `response_format` | object | no |  | JSON schema for structured output |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "The question or research task"
    },
    "preset": {
      "type": "string",
      "description": "Preset to use (default 'pro-search')",
      "default": "pro-search"
    },
    "model": {
      "type": "string",
      "description": "Override the model the preset would pick"
    },
    "instructions": {
      "type": "string",
      "description": "System-level instructions for the agent"
    },
    "language_preference": {
      "type": "string",
      "description": "Preferred answer language, e.g. 'de'"
    },
    "max_output_tokens": {
      "type": "integer",
      "description": "Cap the answer length"
    },
    "max_steps": {
      "type": "integer",
      "description": "Cap how many research steps the agent may take"
    },
    "response_format": {
      "type": "object",
      "description": "JSON schema for structured output"
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

Agentic answer: 'output_text' holds the answer; 'citations' lists sources; 'usage' reports tokens

Key fields: `output_text`, `citations[].url`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing PERPLEXITY_API_KEY | Skip Perplexity tools, use Exa or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 60s and retry once |

## When to use

- Use for complex research that benefits from deeper agent-driven exploration
- No domain or recency filtering here — use perplexity_search or perplexity_chat for that

## Alternatives

_None listed._

## Provider docs

https://docs.perplexity.ai/api-reference
