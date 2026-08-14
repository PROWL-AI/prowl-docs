---
name: keywords_everywhere_unique_domain_backlinks
provider: Keywords Everywhere
provider_slug: keywords_everywhere
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `keywords_everywhere_unique_domain_backlinks`

Top backlinks for a domain, de-duplicated to one link per referring domain — the referring-domain footprint rather than the raw link list.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Keywords Everywhere |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `backlinks`, `domain`, `keywords`, `keywords-everywhere`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "keywords_everywhere_unique_domain_backlinks",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Root domain, e.g. example.com (no scheme) |
| `num` | integer | no | `100` | Maximum results to return (1-10000). Each returned row costs credits — request only what the analysis needs. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Root domain, e.g. example.com (no scheme)"
    },
    "num": {
      "type": "integer",
      "default": 100,
      "minimum": 1,
      "maximum": 10000,
      "description": "Maximum results to return (1-10000). Each returned row costs credits \u2014 request only what the analysis needs."
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

data[] backlink rows, one per referring domain, + credit accounting

Key fields: `data[].anchor_text`, `data[].domain_source`, `data[].url_source`, `data[].url_target`, `credits_consumed`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| invalid_api_key | HTTP 401 — the API key is missing or rejected ('401 Missing Or Invalid API Key'). | Set KEYWORDS_EVERYWHERE_API_KEY to the key from the Keywords Everywhere account page. |
| insufficient_credits | HTTP 402 — no valid subscription, or the credit balance cannot cover the request. | Check the balance with keywords_everywhere_credits; top up credits or lower `num` / the batch size. |
| invalid_request | HTTP 400 — malformed parameters (bad country/currency code, out-of-range num, empty batch). | Validate the country code against keywords_everywhere_countries and keep num within 1-10000. |
| rate_limit | HTTP 429 — too many requests in flight for the account. | Retry with backoff; the provider pool already throttles concurrency for this provider. |
| transient_upstream | HTTP 5xx / timeout / connection error. Handlers return None so the DAG can retry or fall back. | Retry the step; cross-check with dataforseo_* or majestic_* equivalents if it persists. |

## When to use

- 5x the credit cost of the raw variant — keep num tight and treat this as the link-gap sampling tool
- Cross-check the referring-domain count with majestic_get_ref_domains / dataforseo_bl_referring_domains

## Alternatives

- `dataforseo_bl_referring_domains`
- `majestic_get_ref_domains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://api.keywordseverywhere.com/docs/
