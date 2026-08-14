---
name: moz_brand_authority
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_brand_authority`

Moz Brand Authority (1-100) for a domain — how well-known the brand is, measured from branded search demand and mentions rather than links.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Moz |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `moz`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "moz_brand_authority",
  "params": {
    "query": "nike.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Root domain (e.g. nike.com) |
| `scope` | enum(domain, subdomain, subfolder, url) | no | `domain` | Query scope: 'domain' (root domain), 'subdomain', 'subfolder', or 'url' (exact page) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Root domain (e.g. nike.com)"
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
  "query": "nike.com"
}
```

## Output

brand_authority score for the domain

Key fields: `site_metrics.brand_authority`

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

- Brand Authority is domain-level — passing a URL or subdomain still scores the root domain
- Pair with moz_site_metrics to contrast brand strength against link strength

## Alternatives

_None listed._

## Provider docs

https://moz.com/api/docs
