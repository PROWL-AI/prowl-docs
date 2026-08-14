---
name: moz_site_metrics_multiple
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_site_metrics_multiple`

Batched Domain Authority / Spam Score for up to 50 sites in ONE call — the efficient way to profile a competitive set or a donor-link list.

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
  "tool_name": "moz_site_metrics_multiple",
  "params": {
    "queries": [
      "moz.com",
      "ahrefs.com",
      "semrush.com"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `queries` | string[] | yes |  | Domains / subdomains / URLs to profile (batch up to 50) |
| `scope` | enum(domain, subdomain, subfolder, url) | no | `domain` | Query scope: 'domain' (root domain), 'subdomain', 'subfolder', or 'url' (exact page) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "queries": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "maxItems": 50,
      "description": "Domains / subdomains / URLs to profile (batch up to 50)"
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
    "queries"
  ]
}
```

## Example request

```json
{
  "queries": [
    "moz.com",
    "ahrefs.com",
    "semrush.com"
  ]
}
```

## Output

results_by_site[] plus errors_by_site[] for entries Moz could not resolve

Key fields: `results_by_site[].site_query.original_site_query.query`, `results_by_site[].site_metrics.domain_authority`, `results_by_site[].site_metrics.spam_score`, `errors_by_site`

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

- A site missing from results_by_site is a per-site miss, not a call failure — degrade that one site only
- Each site in the batch bills one Moz row

## Alternatives

_None listed._

## Provider docs

https://moz.com/api/docs
