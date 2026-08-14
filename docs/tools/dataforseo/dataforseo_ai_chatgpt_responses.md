---
name: dataforseo_ai_chatgpt_responses
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_ai_chatgpt_responses`

Get structured ChatGPT responses via DataForSEO — generate AI responses with specific models.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_ai_chatgpt_responses",
  "params": {
    "user_prompt": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `force_web_search` | boolean | no |  | force AI agent to use web search |
| `message_chain` | any[] | no |  | conversation history |
| `system_message` | string | no |  | instructions for the AI behaviour |
| `tag` | string | no |  | user-defined task identifier |
| `top_p` | number | no |  | diversity of the AI response |
| `web_search_city` | string | no |  | city name of the location |
| `web_search_country_iso_code` | string | no |  | ISO country code of the location |
| `user_prompt` | string | yes |  | Prompt for ChatGPT (max 500 chars) |
| `model_name` | string | no |  | ChatGPT model name (e.g. gpt-4.1). See /v3/ai_optimization/chat_gpt/llm_responses/models for available models. |
| `max_output_tokens` | integer | no |  | Max tokens in response (16-4096, default 2048) |
| `temperature` | number | no |  | Randomness 0-2 (default 0.94) |
| `web_search` | boolean | no |  | Enable web search for current information |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "force_web_search": {
      "type": "boolean",
      "description": "force AI agent to use web search"
    },
    "message_chain": {
      "type": "array",
      "description": "conversation history"
    },
    "system_message": {
      "type": "string",
      "description": "instructions for the AI behaviour"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "top_p": {
      "type": "number",
      "description": "diversity of the AI response"
    },
    "web_search_city": {
      "type": "string",
      "description": "city name of the location"
    },
    "web_search_country_iso_code": {
      "type": "string",
      "description": "ISO country code of the location"
    },
    "user_prompt": {
      "type": "string",
      "description": "Prompt for ChatGPT (max 500 chars)"
    },
    "model_name": {
      "type": "string",
      "description": "ChatGPT model name (e.g. gpt-4.1). See /v3/ai_optimization/chat_gpt/llm_responses/models for available models."
    },
    "max_output_tokens": {
      "type": "integer",
      "description": "Max tokens in response (16-4096, default 2048)"
    },
    "temperature": {
      "type": "number",
      "description": "Randomness 0-2 (default 0.94)"
    },
    "web_search": {
      "type": "boolean",
      "description": "Enable web search for current information"
    }
  },
  "required": [
    "user_prompt"
  ]
}
```

## Example request

```json
{
  "user_prompt": "example"
}
```

## Output

Top-level keys: `version`, `status_code`, `status_message`, `time`, `cost`, `tasks_count`, `tasks_error`, `tasks`

| Path | Type | Description |
|------|------|-------------|
| `version` | string |  |
| `status_code` | integer |  |
| `status_message` | string |  |
| `time` | string |  |
| `cost` | number |  |
| `tasks_count` | integer |  |
| `tasks_error` | integer |  |
| `tasks[]` | array<object> |  |
| `tasks[].id` | string |  |
| `tasks[].status_code` | integer |  |
| `tasks[].status_message` | string |  |
| `tasks[].time` | string |  |
| `tasks[].cost` | number |  |
| `tasks[].result_count` | integer |  |
| `tasks[].path[]` | array<string> |  |
| `tasks[].data` | object |  |
| `tasks[].data.api` | string |  |
| `tasks[].data.function` | string |  |
| `tasks[].data.se` | string |  |
| `tasks[].data.user_prompt` | string |  |
| `tasks[].data.model_name` | string |  |
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].model_name` | string |  |
| `tasks[].result[].input_tokens` | integer |  |
| `tasks[].result[].output_tokens` | integer |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260806",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "1.5035 sec.",
  "cost": 0.00102,
  "tasks_count": 1,
  "tasks_error": 0,
  "tasks": [
    {
      "id": "08111840-1544-0612-0000-0f210a276499",
      "status_code": 20000,
      "status_message": "Ok.",
      "time": "1.4945 sec.",
      "cost": 0.00102,
      "result_count": 1,
      "path": [
        "v3",
        "ai_optimization",
        "chat_gpt",
        "llm_responses",
        "live"
      ],
 
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

## Alternatives

- `dataforseo_ai_chatgpt_scraper`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
