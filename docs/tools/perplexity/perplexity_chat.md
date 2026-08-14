---
name: perplexity_chat
provider: Perplexity
provider_slug: perplexity
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `perplexity_chat`

Grounded LLM via Perplexity Chat Completions API.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Perplexity |
| Category | `web` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `perplexity`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "perplexity_chat",
  "params": {
    "messages": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `search_mode` | enum(web, academic, sec) | no |  | Corpus to search. |
| `search_after_date_filter` | string | no |  | Only results published after this date (MM/DD/YYYY). |
| `search_before_date_filter` | string | no |  | Only results published before this date (MM/DD/YYYY). |
| `last_updated_after_filter` | string | no |  | Only results last updated after this date (MM/DD/YYYY). |
| `last_updated_before_filter` | string | no |  | Only results last updated before this date (MM/DD/YYYY). |
| `search_language_filter` | any[] | no |  | Restrict results to these ISO 639-1 language codes. |
| `return_related_questions` | boolean | no |  | Also return suggested follow-up queries. |
| `search_context_size` | enum(low, medium, high) | no |  | How much web context to retrieve; higher costs more. |
| `user_location` | object | no |  | Searcher location, e.g. {'country': 'DE'}. Defaults to the run's market when one was decided. |
| `messages` | object[] | yes |  | Conversation messages |
| `model` | enum(sonar, sonar-pro, sonar-reasoning, sonar-reasoning-pro) | no | `sonar` | Perplexity model to use |
| `search_domain_filter` | string[] | no |  | Domains to include/exclude (prefix with '-' to exclude) |
| `search_recency_filter` | enum(hour, day, week, month) | no |  | Filter results by recency |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "search_mode": {
      "type": "string",
      "description": "Corpus to search.",
      "enum": [
        "web",
        "academic",
        "sec"
      ]
    },
    "search_after_date_filter": {
      "type": "string",
      "description": "Only results published after this date (MM/DD/YYYY)."
    },
    "search_before_date_filter": {
      "type": "string",
      "description": "Only results published before this date (MM/DD/YYYY)."
    },
    "last_updated_after_filter": {
      "type": "string",
      "description": "Only results last updated after this date (MM/DD/YYYY)."
    },
    "last_updated_before_filter": {
      "type": "string",
      "description": "Only results last updated before this date (MM/DD/YYYY)."
    },
    "search_language_filter": {
      "type": "array",
      "description": "Restrict results to these ISO 639-1 language codes."
    },
    "return_related_questions": {
      "type": "boolean",
      "description": "Also return suggested follow-up queries."
    },
    "search_context_size": {
      "type": "string",
      "description": "How much web context to retrieve; higher costs more.",
      "enum": [
        "low",
        "medium",
        "high"
      ]
    },
    "user_location": {
      "type": "object",
      "description": "Searcher location, e.g. {'country': 'DE'}. Defaults to the run's market when one was decided."
    },
    "messages": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "role": {
            "type": "string",
            "enum": [
              "system",
              "user",
              "assistant"
            ]
          },
          "content": {
            "type": "string"
          }
        },
        "required": [
          "role",
          "content"
        ]
      },
      "description": "Conversation messages"
    },
    "model": {
      "type": "string",
      "description": "Perplexity model to use",
      "enum": [
        "sonar",
        "sonar-pro",
        "sonar-reasoning",
        "sonar-reasoning-pro"
      ],
      "default": "sonar"
    },
    "search_domain_filter": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Domains to include/exclude (prefix with '-' to exclude)"
    },
    "search_recency_filter": {
      "type": "string",
      "enum": [
        "hour",
        "day",
        "week",
        "month"
      ],
      "description": "Filter results by recency"
    }
  },
  "required": [
    "messages"
  ]
}
```

## Example request

```json
{
  "messages": []
}
```

## Output

LLM response backed by web search with citations

Key fields: `content`, `citations`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing PERPLEXITY_API_KEY | Skip Perplexity tools, use Exa or Firecrawl alternatives |
| 429 | Rate limit exceeded | Wait 60s and retry once |

## When to use

- Use for conversational Q&A, follow-up questions, or multi-turn analysis
- Models: 'sonar' (fast), 'sonar-pro' (thorough), 'sonar-reasoning' (step-by-step)

**Chain groups:** `perplexity`

## Alternatives

_None listed._

## Provider docs

https://docs.perplexity.ai/api-reference
