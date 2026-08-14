---
name: discover_web_funnels
provider: crt.sh
provider_slug: crt_sh
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `discover_web_funnels`

Comprehensive web funnel discovery for a domain.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | crt.sh |
| Category | `utility` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `crt.sh`, `utility` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "discover_web_funnels",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Domain to discover web funnels for (e.g. 'example.com') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Domain to discover web funnels for (e.g. 'example.com')"
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

Funnel report with URLs grouped by purpose

Key fields: `summary.total_subdomains`, `summary.funnel_subdomains`, `funnel_urls`, `app_urls`, `tracking_urls`, `all_subdomains_by_category`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| timeout | crt.sh is slow or unreachable during funnel discovery | Retry once after 10s; if still fails, fall back to find_subdomains or skip funnel mapping |
| empty | No recent certificates / funnels found for the domain | Treat as no-signal, not a hard failure; try firecrawl_map_domain as an alternative |
| http | Upstream HTTP error from crt.sh | Retry once; if persistent, skip subdomain/funnel discovery for this target |

## When to use

- Recommended first step when analyzing a domain's marketing funnel strategy
- Follow up with foreplay_get_brands_by_domain and foreplay_get_ads_by_brand_ids for ad creatives

## Alternatives

- `find_subdomains`
- `dataforseo_labs_subdomains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://crt.sh
