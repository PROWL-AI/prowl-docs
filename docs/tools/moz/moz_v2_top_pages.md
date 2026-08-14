---
name: moz_v2_top_pages
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_v2_top_pages`

Legacy Links API top pages for a site with full per-page URL metrics, HTTP-status filtering, and optional history series.

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
  "tool_name": "moz_v2_top_pages",
  "params": {
    "target": "moz.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | The domain to return top pages for |
| `scope` | enum(subdomain, root_domain) | no | `root_domain` | Top pages are site-level: subdomain or root_domain only |
| `filter` | enum(all, status_200, status_301, status_302, status_4xx, status_5xx) | no |  | HTTP-status filter (Moz default 'all'); 'status_4xx' finds broken pages that still have links |
| `sort` | enum(page_authority, root_domains_to_page, external_pages_to_page) | no |  | Sort order (Moz default page_authority) |
| `daily_history_deltas` | string[] | no |  | Metrics to return 60-day daily gains/losses for (+1 quota row per entry, per target) |
| `daily_history_values` | string[] | no |  | Metrics to return 60-day daily values for (+1 quota row per entry, per target) |
| `monthly_history_deltas` | string[] | no |  | As daily_history_deltas, over 32 months (+1 quota row per entry, per target) |
| `monthly_history_values` | string[] | no |  | As daily_history_values, over 32 months (+1 quota row per entry, per target) |
| `limit` | integer | no | `25` | Max rows to return (1-50); every returned row bills Moz quota — this is the cost dial |
| `next_token` | string | no |  | Pagination cursor |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "The domain to return top pages for"
    },
    "scope": {
      "type": "string",
      "enum": [
        "subdomain",
        "root_domain"
      ],
      "default": "root_domain",
      "description": "Top pages are site-level: subdomain or root_domain only"
    },
    "filter": {
      "type": "string",
      "enum": [
        "all",
        "status_200",
        "status_301",
        "status_302",
        "status_4xx",
        "status_5xx"
      ],
      "description": "HTTP-status filter (Moz default 'all'); 'status_4xx' finds broken pages that still have links"
    },
    "sort": {
      "type": "string",
      "enum": [
        "page_authority",
        "root_domains_to_page",
        "external_pages_to_page"
      ],
      "description": "Sort order (Moz default page_authority)"
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

Top-page rows

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

- filter='status_4xx' + sort='root_domains_to_page' ranks link reclamation by how much equity is stranded
- History modifiers add rows exactly as in moz_v2_url_metrics

## Alternatives

- `spyfu_get_new_top_pages`
- `spyfu_get_top_pages`
- `keywords_everywhere_page_backlinks`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://moz.com/help/links-api
