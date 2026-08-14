---
name: dataforseo_domain_technology_stats
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_domain_technology_stats`

Get historical technology adoption stats — track how technology usage changes over time.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `domain`, `technographics` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_domain_technology_stats",
  "params": {
    "technology": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `tag` | string | no |  | user-defined task identifier |
| `technology` | string | yes |  | Technology name (e.g. 'WordPress', 'React') |
| `date_from` | string | no |  | Start date (YYYY-MM-DD) |
| `date_to` | string | no |  | End date (YYYY-MM-DD) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "technology": {
      "type": "string",
      "description": "Technology name (e.g. 'WordPress', 'React')"
    },
    "date_from": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD)"
    },
    "date_to": {
      "type": "string",
      "description": "End date (YYYY-MM-DD)"
    }
  },
  "required": [
    "technology"
  ]
}
```

## Example request

```json
{
  "technology": "example"
}
```

## Output

_No output schema or active profile response_format._

> Profile capture status: **error** — DataForSEOError: DataForSEO task errors: 40501: Invalid Field: 'technology'.

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

- `dataforseo_domain_domains_by_technology`
- `dataforseo_ai_llm_mentions_top_domains`
- `dataforseo_domain_technologies`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
