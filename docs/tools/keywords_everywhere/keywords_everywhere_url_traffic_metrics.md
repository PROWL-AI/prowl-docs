---
name: keywords_everywhere_url_traffic_metrics
provider: Keywords Everywhere
provider_slug: keywords_everywhere
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `keywords_everywhere_url_traffic_metrics`

Batch traffic snapshot for a list of URLs: estimated monthly organic traffic and total top-30 ranking keywords per page.

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
  "tool_name": "keywords_everywhere_url_traffic_metrics",
  "params": {
    "urls": [
      "https://example.com/",
      "https://example.com/pricing"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `urls` | string[] | yes |  | Full URLs including scheme |
| `country` | string | no | `us` | Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "urls": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "description": "Full URLs including scheme"
    },
    "country": {
      "type": "string",
      "default": "us",
      "description": "Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data."
    }
  },
  "required": [
    "urls"
  ]
}
```

## Example request

```json
{
  "urls": [
    "https://example.com/",
    "https://example.com/pricing"
  ]
}
```

## Output

data[] rows (one per requested URL) + credit accounting

Key fields: `data[].url`, `data[].estimated_monthly_traffic`, `data[].total_ranking_keywords`, `credits_consumed`

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

- Feed it a sitemap slice or the URLs returned by firecrawl_map_domain to find a competitor's traffic-carrying pages

## Alternatives

- `dataforseo_labs_bulk_traffic_estimation`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://api.keywordseverywhere.com/docs/
