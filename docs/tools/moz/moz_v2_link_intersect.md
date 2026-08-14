---
name: moz_v2_link_intersect
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_v2_link_intersect`

Link-gap analysis: sources that link to the competitors in `positive_targets` but to none in `negative_targets`.

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
  "tool_name": "moz_v2_link_intersect",
  "params": {
    "positive_targets": [
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
| `positive_targets` | string[] | yes |  | Competitor domains the prospects must link to (max 6 across positive + negative) |
| `negative_targets` | string[] | no |  | Domains the prospects must NOT link to — usually the client |
| `scope` | enum(page, subdomain, root_domain) | no | `root_domain` | Query scope: 'page' (exact URL), 'subdomain', or 'root_domain' |
| `source_scope` | enum(page, root_domain) | no |  | Scope of the linking sources (Moz default 'page') |
| `min_matching_targets` | integer | no |  | Only return sources matching at least this many positive targets |
| `sort` | enum(matching_target_count, source_domain_authority, source_spam_score) | no |  | Sort order (Moz default matching_target_count) |
| `limit` | integer | no | `25` | Max rows to return (1-50); every returned row bills Moz quota — this is the cost dial |
| `next_token` | string | no |  | Pagination cursor |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "positive_targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "maxItems": 6,
      "description": "Competitor domains the prospects must link to (max 6 across positive + negative)"
    },
    "negative_targets": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "maxItems": 6,
      "description": "Domains the prospects must NOT link to \u2014 usually the client"
    },
    "scope": {
      "type": "string",
      "enum": [
        "page",
        "subdomain",
        "root_domain"
      ],
      "default": "root_domain",
      "description": "Query scope: 'page' (exact URL), 'subdomain', or 'root_domain'"
    },
    "source_scope": {
      "type": "string",
      "enum": [
        "page",
        "root_domain"
      ],
      "description": "Scope of the linking sources (Moz default 'page')"
    },
    "min_matching_targets": {
      "type": "integer",
      "minimum": 1,
      "description": "Only return sources matching at least this many positive targets"
    },
    "sort": {
      "type": "string",
      "enum": [
        "matching_target_count",
        "source_domain_authority",
        "source_spam_score"
      ],
      "description": "Sort order (Moz default matching_target_count)"
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
    "positive_targets"
  ]
}
```

## Example request

```json
{
  "positive_targets": [
    "ahrefs.com",
    "semrush.com"
  ]
}
```

## Output

Prospect rows

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

- Put the client in negative_targets — otherwise the list is full of sites that already link to them
- 5 rows per RETURNED result: limit=50 costs 250 quota rows. Start at limit=10 and widen only if the list is thin
- min_matching_targets=2 keeps the list broad; 3+ narrows it to the strongest signals

## Alternatives

_None listed._

## Provider docs

https://moz.com/help/links-api
