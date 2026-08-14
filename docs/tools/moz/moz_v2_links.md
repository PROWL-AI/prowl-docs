---
name: moz_v2_links
provider: Moz
provider_slug: moz
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `moz_v2_links`

Legacy Links API backlink pull with the filters v3 has no equivalent for: follow/nofollow/deleted filtering, sort by source authority or spam score, anchor-text match, and sourc...

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
  "tool_name": "moz_v2_links",
  "params": {
    "target": "moz.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `target` | string | yes |  | Domain, subdomain, or URL to pull backlinks for |
| `target_scope` | enum(page, subdomain, root_domain) | no | `root_domain` | Query scope: 'page' (exact URL), 'subdomain', or 'root_domain' |
| `source_scope` | enum(page, subdomain, root_domain) | no |  | Scope of the linking sources; at subdomain/root_domain Moz returns only the best link per source |
| `filter` | enum(external, external+follow, external+nofollow, external+deleted, external+not_redirect) | no |  | Link filter (Moz default 'external'); 'external+follow' is the equity-passing subset |
| `sort` | enum(source_page_authority, source_domain_authority, source_spam_score, source_link_propensity, root_domains_to_source_page, root_domains_to_source_root_domain) | no |  | Sort order (Moz default source_page_authority) |
| `anchor_text` | string | no |  | Only links whose normalised anchor text equals this |
| `source_root_domain` | string | no |  | Only links from this source root domain |
| `subdomains_limited_to_one` | string[] | no |  | Return only the best link from each listed subdomain |
| `limit` | integer | no | `25` | Max rows to return (1-50); every returned row bills Moz quota — this is the cost dial |
| `next_token` | string | no |  | Pagination cursor from the previous response |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "target": {
      "type": "string",
      "description": "Domain, subdomain, or URL to pull backlinks for"
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
    "source_scope": {
      "type": "string",
      "enum": [
        "page",
        "subdomain",
        "root_domain"
      ],
      "description": "Scope of the linking sources; at subdomain/root_domain Moz returns only the best link per source"
    },
    "filter": {
      "type": "string",
      "enum": [
        "external",
        "external+follow",
        "external+nofollow",
        "external+deleted",
        "external+not_redirect"
      ],
      "description": "Link filter (Moz default 'external'); 'external+follow' is the equity-passing subset"
    },
    "sort": {
      "type": "string",
      "enum": [
        "source_page_authority",
        "source_domain_authority",
        "source_spam_score",
        "source_link_propensity",
        "root_domains_to_source_page",
        "root_domains_to_source_root_domain"
      ],
      "description": "Sort order (Moz default source_page_authority)"
    },
    "anchor_text": {
      "type": "string",
      "description": "Only links whose normalised anchor text equals this"
    },
    "source_root_domain": {
      "type": "string",
      "description": "Only links from this source root domain"
    },
    "subdomains_limited_to_one": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Return only the best link from each listed subdomain"
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
      "description": "Pagination cursor from the previous response"
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

results[] link rows plus next_token

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

- filter='external+follow' sorted by source_domain_authority is the shortest path to links that pass equity
- Page with next_token instead of raising limit — every row bills, and the cap is 50
- Not every sort/filter combines with anchor_text, source_root_domain, or subdomains_limited_to_one

## Alternatives

_None listed._

## Provider docs

https://moz.com/help/links-api
