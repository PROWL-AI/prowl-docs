---
name: moz_v2_url_metrics
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_v2_url_metrics`

Legacy Moz Links API: batched DA/PA/Spam Score for up to 50 targets, with optional daily and monthly HISTORY series — the only Moz surface that returns authority over TIME rathe...

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
  "tool_name": "moz_v2_url_metrics",
  "params": {
    "targets": [
      "moz.com"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `targets` | string[] | yes |  | 1-50 URLs or domains; a bare domain is treated as that page |
| `distributions` | boolean | no |  | Add link-distribution histograms bucketed by root domains / DA / spam score (+1 quota row per target) |
| `daily_history_deltas` | string[] | no |  | Metrics to return 60-day daily gains/losses for (+1 quota row per entry, per target) |
| `daily_history_values` | string[] | no |  | Metrics to return 60-day daily values for (+1 quota row per entry, per target) |
| `monthly_history_deltas` | string[] | no |  | As daily_history_deltas, over 32 months (+1 quota row per entry, per target) |
| `monthly_history_values` | string[] | no |  | As daily_history_values, over 32 months (+1 quota row per entry, per target) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "maxItems": 50,
      "description": "1-50 URLs or domains; a bare domain is treated as that page"
    },
    "distributions": {
      "type": "boolean",
      "description": "Add link-distribution histograms bucketed by root domains / DA / spam score (+1 quota row per target)"
    },
    "daily_history_deltas": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Metrics to return 60-day daily gains/losses for (+1 quota row per entry, per target)"
    },
    "daily_history_values": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Metrics to return 60-day daily values for (+1 quota row per entry, per target)"
    },
    "monthly_history_deltas": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "As daily_history_deltas, over 32 months (+1 quota row per entry, per target)"
    },
    "monthly_history_values": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "As daily_history_values, over 32 months (+1 quota row per entry, per target)"
    }
  },
  "required": [
    "targets"
  ]
}
```

## Example request

```json
{
  "targets": [
    "moz.com"
  ]
}
```

## Output

results[] with one metric object per target

Key fields: `results[].domain_authority`, `results[].page_authority`, `results[].spam_score`, `results[].root_domains_to_root_domain`, `results[].pages_to_root_domain`

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

- History series are what v3 cannot do — reach for this when the question is 'did authority move?'
- Weighted endpoint: 1 row per target, plus 1 more per target for distributions and per history entry
- You cannot select which base metrics come back — all are returned per target
- A 401 here while moz_site_metrics works means a v3 token but no Links API subscription

## Alternatives

_None listed._

## Provider docs

https://moz.com/help/links-api
