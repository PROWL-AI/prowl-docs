---
name: keywords_everywhere_url_keywords
provider: Keywords Everywhere
provider_slug: keywords_everywhere
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `keywords_everywhere_url_keywords`

Keywords a single URL ranks for, with estimated monthly traffic and SERP position per keyword — page-level counterpart to keywords_everywhere_domain_keywords.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Keywords Everywhere |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `keywords`, `keywords-everywhere`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "keywords_everywhere_url_keywords",
  "params": {
    "url": "https://example.com/"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Full URL including scheme, e.g. https://example.com/pricing |
| `country` | string | no | `us` | Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data. |
| `num` | integer | no | `100` | Maximum results to return (1-10000). Each returned row costs credits — request only what the analysis needs. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Full URL including scheme, e.g. https://example.com/pricing"
    },
    "country": {
      "type": "string",
      "default": "us",
      "description": "Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data."
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
    "url"
  ]
}
```

## Example request

```json
{
  "url": "https://example.com/"
}
```

## Output

data[] rows of ranked keywords for the URL + credit accounting

Key fields: `data[].keyword`, `data[].estimated_monthly_traffic`, `data[].serp_position`, `credits_consumed`

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

- Use on a competitor's top landing page to reverse-engineer what that page is built to rank for
- Per-site result caps are plan-bound: 1,000 (Bronze) / 2,000 (Silver) / 5,000 (Gold) / 10,000 (Platinum)

## Alternatives

- `dataforseo_labs_ranked_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://api.keywordseverywhere.com/docs/
