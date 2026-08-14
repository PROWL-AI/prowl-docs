---
name: moz_keyword_suggestions
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_keyword_suggestions`

Related keyword suggestions for a seed term, with Moz metrics attached — keyword expansion from a third index next to keywords_everywhere_related and dataforseo_keyword_suggesti...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Moz |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `keywords`, `moz`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "moz_keyword_suggestions",
  "params": {
    "keyword": "seo tools"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keyword` | string | yes |  | Seed keyword |
| `locale` | string | no | `en-US` | Locale, e.g. en-US, en-GB, de-DE |
| `limit` | integer | no | `25` | Max rows to return (1-1000); every returned row bills Moz quota |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keyword": {
      "type": "string",
      "description": "Seed keyword"
    },
    "locale": {
      "type": "string",
      "default": "en-US",
      "description": "Locale, e.g. en-US, en-GB, de-DE"
    },
    "limit": {
      "type": "integer",
      "default": 25,
      "minimum": 1,
      "maximum": 1000,
      "description": "Max rows to return (1-1000); every returned row bills Moz quota"
    }
  },
  "required": [
    "keyword"
  ]
}
```

## Example request

```json
{
  "keyword": "seo tools"
}
```

## Output

suggestions[] rows

Key fields: `suggestions`, `page`, `options`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| invalid_api_key | HTTP 401/403 — the Moz credential is missing or rejected. | Set MOZ_API_TOKEN — verified to authenticate BOTH the v3 JSON-RPC API (x-moz-token) and the v2 Links API. The legacy MOZ_ACCESS_ID + MOZ_SECRET_KEY Basic pair is an optional override, not a requirement. |
| quota_exceeded | The account's monthly row quota is exhausted (Moz throttles/rejects rather than overcharging). | Check the balance with moz_quota; lower `limit`, batch fewer sites, or wait for the monthly reset. |
| invalid_request | HTTP 400 or a JSON-RPC error — malformed method params, bad scope, or an unparseable target. | Pass a bare root domain (example.com) or full URL and a scope from page\|subdomain\|root_domain. |
| rate_limit | HTTP 429 — too many requests in flight for the account. | Retry with backoff; the provider pool already throttles concurrency for this provider. |
| transient_upstream | HTTP 5xx / timeout / connection error. Handlers return None so the DAG can retry or fall back. | Retry the step; cross-check with majestic_* or dataforseo_bl_* equivalents if it persists. |

## When to use

- Each suggestion row bills quota — pull a tight list and expand only the survivors

## Alternatives

- `spyfu_competing_ppc_keywords`
- `spyfu_competing_seo_keywords`
- `spyfu_find_also_buys_ads_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://moz.com/api/docs
