---
name: exa_research
provider: Exa
provider_slug: exa
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `exa_research`

Deep research via Exa Research API.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Exa |
| Category | `web` |
| Timeout | 180 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `exa`, `search`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "exa_research",
  "params": {
    "instructions": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `instructions` | string | yes |  | Detailed research instructions/question |
| `output_schema` | object | no |  | Optional JSON schema for structured output |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "instructions": {
      "type": "string",
      "description": "Detailed research instructions/question"
    },
    "output_schema": {
      "type": "object",
      "description": "Optional JSON schema for structured output"
    }
  },
  "required": [
    "instructions"
  ]
}
```

## Example request

```json
{
  "instructions": "example"
}
```

## Output

Research result: 'output' holds the report text (with inline citations); 'parsed' holds structured output when an output_schema was supplied; 'cost_dollars' reports the spend.

Key fields: `output`, `parsed`, `cost_dollars.total`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing EXA_API_KEY | Skip Exa tools, use Perplexity or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 30s and retry once |

## When to use

- Use for complex multi-step research tasks (e.g. 'Compare pricing models of top 5 CRM platforms')
- Provide output_schema for structured JSON output; without it, returns free-text result
- Internally polls for up to 120s — may take longer than other tools

## Alternatives

- `firecrawl_search`
- `perplexity_search`
- `perplexity_search_by_query`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.exa.ai
