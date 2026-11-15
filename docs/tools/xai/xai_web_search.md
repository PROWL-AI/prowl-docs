---
name: xai_web_search
provider: xAI
provider_slug: xai
category: web
generated_at: 2026-11-15T23:06:03Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `xai_web_search`

Agentic web search through xAI Grok with citations; optionally adds X (Twitter) search to the same call.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | xAI |
| Category | `web` |
| Timeout | 180 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `xai`, `web`, `search` |
| Last schema check | `PASS` — 2026-11-15T19:45:00Z |
| Last live API check | `PASS` — 2026-11-15T19:45:00 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "xai_web_search",
  "params": {
    "query": "Which eSIM providers launched new travel plans in November 2026?"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Natural-language question or research task. |
| `allowed_domains` | string[] | no |  | Search and browse only these domains (max 5). Not with excluded_domains. |
| `excluded_domains` | string[] | no |  | Keep these domains out of the search (max 5). Not with allowed_domains. |
| `include_x` | boolean | no | `False` | Also search X (Twitter) posts in the same call. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Natural-language question or research task."
    },
    "allowed_domains": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "maxItems": 5,
      "description": "Search and browse only these domains (max 5). Not with excluded_domains."
    },
    "excluded_domains": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "maxItems": 5,
      "description": "Keep these domains out of the search (max 5). Not with allowed_domains."
    },
    "include_x": {
      "type": "boolean",
      "default": false,
      "description": "Also search X (Twitter) posts in the same call."
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
  "query": "Which eSIM providers launched new travel plans in November 2026?"
}
```

## Output

Grok's answer with its sources: 'answer' (text), 'citations' [{url, title}], 'x_post_urls' (the x.com subset), 'transport' ('xai' | 'openrouter'), 'model', 'usage' (tokens, x_posts_fetched when reported) and 'cost_usd' (what the call cost).

Key fields: `answer`, `citations[].url`, `x_post_urls`, `transport`, `model`, `usage`, `cost_usd`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| no_credential | Neither XAI_API_KEY nor OPENROUTER_API_KEY is set (auth class, no network call made). | Set XAI_API_KEY (direct xAI) or OPENROUTER_API_KEY (fallback); otherwise use perplexity_chat or reddit_search. |
| 401 | The key was rejected by xAI or OpenRouter (unauthorized). | Check the key the transport named in `transport`; do not retry. |
| 429 | Rate limit exceeded at xAI or OpenRouter. | Wait 60s and retry once. |
| invalid_params | Bad input: dates not YYYY-MM-DD, from_date not before to_date, too many handles or domains, or allowed and excluded lists both set. | Fix the arguments; the message names the field. |

## When to use

- Use include_x when the web answer should also reflect what people post on X.
- For plain web Q&A with recency filters perplexity_chat is cheaper; use this when Grok's reading of X matters.

## Alternatives

- `perplexity_chat`
- `exa_answer`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.x.ai/developers/tools/web-search
