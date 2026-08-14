---
name: foreplay_get_brands_by_domain
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_get_brands_by_domain`

Find advertising brands associated with a domain via Foreplay.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `domain`, `foreplay` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_get_brands_by_domain",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Domain name (e.g. 'example.com') |
| `limit` | integer | no | `10` | Max brands to return |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Domain name (e.g. 'example.com')"
    },
    "limit": {
      "type": "integer",
      "description": "Max brands to return",
      "default": 10,
      "minimum": 1,
      "maximum": 10
    }
  },
  "required": [
    "domain"
  ]
}
```

## Example request

```json
{
  "domain": "example.com"
}
```

## Output

Brands for domain with enriched URLs

Key fields: `data[].id`, `data[].name`, `data[].facebook_page_url`, `data[].ad_library_url`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |
| excluded_domain | Domain is blocked/excluded by Foreplay | Use foreplay_discovery_brands with the brand name instead |

## When to use

- Primary way to discover a domain's advertising activity
- Follow up with foreplay_get_ads_by_brand_ids using the returned brand IDs

**Chain groups:** `foreplay`

## Alternatives

- `foreplay_discovery_ads`
- `foreplay_discovery_brands`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.foreplay.co
