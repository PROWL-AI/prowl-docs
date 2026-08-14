---
name: find_subdomains
provider: crt.sh
provider_slug: crt_sh
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `find_subdomains`

Discover recently active subdomains for a domain using certificate transparency logs (crt.sh).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | crt.sh |
| Category | `utility` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `crt.sh`, `domain`, `utility` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "find_subdomains",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Domain to discover subdomains for (e.g. 'example.com') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Domain to discover subdomains for (e.g. 'example.com')"
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

Structured subdomain report with classified URLs

Key fields: `subdomains[].subdomain`, `subdomains[].url`, `subdomains[].category`, `funnel_urls`, `app_urls`, `tracking_urls`, `total_count`, `funnel_count`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| timeout | crt.sh is slow or unreachable | Retry once after 10s; if still fails, skip subdomain discovery |

## When to use

- Results come from certificate transparency — only subdomains with SSL certs in the last 60 days
- Combine with firecrawl_map_domain for a fuller picture of the domain's pages

## Alternatives

- `discover_web_funnels`
- `dataforseo_labs_subdomains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://crt.sh
