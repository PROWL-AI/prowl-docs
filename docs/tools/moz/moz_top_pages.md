---
name: moz_top_pages
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_top_pages`

Highest-authority pages on a target site, ranked by Page Authority and link equity — the fastest read on which content actually earns a competitor's links.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Moz |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `moz`, `onpage`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "moz_top_pages",
  "params": {
    "target": "moz.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | Domain or subdomain |
| `scope` | enum(domain, subdomain, subfolder, url) | no | `domain` | Query scope: 'domain' (root domain), 'subdomain', 'subfolder', or 'url' (exact page) |
| `limit` | integer | no | `25` | Max rows to return (1-1000); every returned row bills Moz quota |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "Domain or subdomain"
    },
    "scope": {
      "type": "string",
      "enum": [
        "domain",
        "subdomain",
        "subfolder",
        "url"
      ],
      "default": "domain",
      "description": "Query scope: 'domain' (root domain), 'subdomain', 'subfolder', or 'url' (exact page)"
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
    "target"
  ]
}
```

## Example request

```json
{
  "target": "moz.com"
}
```

## Output

top_pages[] rows

Key fields: `top_pages`, `offset`, `options`

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

- Pair with moz_ranking_keywords to see which of those pages also convert to rankings

## Alternatives

- `spyfu_get_new_top_pages`
- `spyfu_get_top_pages`
- `keywords_everywhere_page_backlinks`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://moz.com/api/docs
