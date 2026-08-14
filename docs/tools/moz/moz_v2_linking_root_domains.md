---
name: moz_v2_linking_root_domains
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_v2_linking_root_domains`

Legacy Links API referring domains with LINK VELOCITY: filter to domains gained or lost in the last 60 days, or sort by date_gained/date_lost over an explicit window.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Moz |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `domain`, `moz`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "moz_v2_linking_root_domains",
  "params": {
    "target": "moz.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | Domain, subdomain, or URL |
| `target_scope` | enum(page, subdomain, root_domain) | no | `root_domain` | Query scope: 'page' (exact URL), 'subdomain', or 'root_domain' |
| `filter` | enum(external, external+follow, external+nofollow, external+deleted, external+not_deleted, external+gained_last_60_days, external+lost_last_60_days) | no |  | Filter (Moz default 'external'); the gained/lost variants are the velocity read |
| `sort` | enum(source_domain_authority, source_link_propensity, source_spam_score, date_gained, date_lost) | no |  | Sort order (Moz default source_domain_authority) |
| `begin_date` | string | no |  | Window start YYYY-MM-DD — only valid with sort=date_gained\|date_lost |
| `end_date` | string | no |  | Window end YYYY-MM-DD — only valid with sort=date_gained\|date_lost |
| `limit` | integer | no | `25` | Max rows to return (1-50); every returned row bills Moz quota — this is the cost dial |
| `next_token` | string | no |  | Pagination cursor |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "Domain, subdomain, or URL"
    },
    "target_scope": {
      "type": "string",
      "enum": [
        "page",
        "subdomain",
        "root_domain"
      ],
      "default": "root_domain",
      "description": "Query scope: 'page' (exact URL), 'subdomain', or 'root_domain'"
    },
    "filter": {
      "type": "string",
      "enum": [
        "external",
        "external+follow",
        "external+nofollow",
        "external+deleted",
        "external+not_deleted",
        "external+gained_last_60_days",
        "external+lost_last_60_days"
      ],
      "description": "Filter (Moz default 'external'); the gained/lost variants are the velocity read"
    },
    "sort": {
      "type": "string",
      "enum": [
        "source_domain_authority",
        "source_link_propensity",
        "source_spam_score",
        "date_gained",
        "date_lost"
      ],
      "description": "Sort order (Moz default source_domain_authority)"
    },
    "begin_date": {
      "type": "string",
      "description": "Window start YYYY-MM-DD \u2014 only valid with sort=date_gained|date_lost"
    },
    "end_date": {
      "type": "string",
      "description": "Window end YYYY-MM-DD \u2014 only valid with sort=date_gained|date_lost"
    },
    "limit": {
      "type": "integer",
      "default": 25,
      "minimum": 1,
      "maximum": 50,
      "description": "Max rows to return (1-50); every returned row bills Moz quota \u2014 this is the cost dial"
    },
    "next_token": {
      "type": "string",
      "description": "Pagination cursor"
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

Linking root-domain rows

Key fields: `results`, `next_token`

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

- Positive filters need ONE matching link from the source domain; negative filters need ALL its links to match
- A date window without a date sort is rejected client-side here — Moz would 400 it

## Alternatives

- `spyfu_find_matching_domains`
- `spyfu_get_all_domain_stats`
- `spyfu_get_bulk_domain_stats`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://moz.com/help/links-api
