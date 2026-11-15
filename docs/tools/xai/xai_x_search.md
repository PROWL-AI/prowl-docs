---
name: xai_x_search
provider: xAI
provider_slug: xai
category: web
generated_at: 2026-11-15T23:06:03Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `xai_x_search`

Search X (Twitter) posts and trends through xAI Grok's agentic X search; answers with the posts as citations.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | xAI |
| Category | `web` |
| Timeout | 180 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `xai`, `social`, `trends`, `search` |
| Last schema check | `PASS` — 2026-11-15T19:45:00Z |
| Last live API check | `PASS` — 2026-11-15T19:45:00 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "xai_x_search",
  "params": {
    "query": "What are people on X saying about eSIM apps for travel this month?"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Natural-language question, e.g. 'What are people on X saying about eSIM apps this week?' |
| `from_date` | string | no |  | Only posts on or after this date, YYYY-MM-DD (00:00 UTC). |
| `to_date` | string | no |  | Only posts before this date, YYYY-MM-DD (exclusive: for one day pass the next day). |
| `allowed_x_handles` | string[] | no |  | Search only these X handles (no @, max 20). Not with excluded_x_handles. |
| `excluded_x_handles` | string[] | no |  | Leave out these X handles (no @, max 20). Not with allowed_x_handles. |
| `enable_image_understanding` | boolean | no | `False` | Let Grok read images in posts (billed as image tokens). |
| `enable_video_understanding` | boolean | no | `False` | Let Grok read videos in posts (billed as tokens). |
| `max_turns` | integer | no |  | Cap the search rounds (direct xAI only; the OpenRouter fallback ignores it and says so). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Natural-language question, e.g. 'What are people on X saying about eSIM apps this week?'"
    },
    "from_date": {
      "type": "string",
      "description": "Only posts on or after this date, YYYY-MM-DD (00:00 UTC)."
    },
    "to_date": {
      "type": "string",
      "description": "Only posts before this date, YYYY-MM-DD (exclusive: for one day pass the next day)."
    },
    "allowed_x_handles": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "maxItems": 20,
      "description": "Search only these X handles (no @, max 20). Not with excluded_x_handles."
    },
    "excluded_x_handles": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "maxItems": 20,
      "description": "Leave out these X handles (no @, max 20). Not with allowed_x_handles."
    },
    "enable_image_understanding": {
      "type": "boolean",
      "default": false,
      "description": "Let Grok read images in posts (billed as image tokens)."
    },
    "enable_video_understanding": {
      "type": "boolean",
      "default": false,
      "description": "Let Grok read videos in posts (billed as tokens)."
    },
    "max_turns": {
      "type": "integer",
      "minimum": 1,
      "description": "Cap the search rounds (direct xAI only; the OpenRouter fallback ignores it and says so)."
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
  "query": "What are people on X saying about eSIM apps for travel this month?"
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

- Use for social trends, sentiment and launch reactions on X; llm_query_grok answers from training data and does not search.
- Set from_date for anything time-bound: without it Grok may cite old posts.
- Billed per X post read plus tokens, so one well-scoped question beats several narrow ones.

## Alternatives

- `reddit_search`
- `perplexity_chat`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.x.ai/developers/tools/x-search
