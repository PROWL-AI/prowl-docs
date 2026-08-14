---
name: keywords_everywhere_domain_traffic_metrics
provider: Keywords Everywhere
provider_slug: keywords_everywhere
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `keywords_everywhere_domain_traffic_metrics`

Batch traffic snapshot for a list of domains: estimated monthly organic traffic and the total number of keywords ranking in the top 30, per country.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Keywords Everywhere |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `domain`, `keywords`, `keywords-everywhere`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "keywords_everywhere_domain_traffic_metrics",
  "params": {
    "domains": [
      "example.com",
      "example.org"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domains` | string[] | yes |  | Root domains to compare, e.g. ['example.com', 'competitor.com'] |
| `country` | string | no | `us` | Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domains": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "description": "Root domains to compare, e.g. ['example.com', 'competitor.com']"
    },
    "country": {
      "type": "string",
      "default": "us",
      "description": "Country code from keywords_everywhere_countries (us, uk, ca, au, in, nz, za). Empty string = global data."
    }
  },
  "required": [
    "domains"
  ]
}
```

## Example request

```json
{
  "domains": [
    "example.com",
    "example.org"
  ]
}
```

## Output

data[] rows (one per requested domain) + credit accounting

Key fields: `data[].domain`, `data[].estimated_monthly_traffic`, `data[].total_ranking_keywords`, `credits_consumed`

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

- Batch the whole competitor set in one call — cost is per domain either way, latency is not
- Pair with keywords_everywhere_domain_keywords on the winners only, to keep credit spend bounded

## Alternatives

- `dataforseo_labs_bulk_traffic_estimation`
- `spyfu_get_bulk_domain_stats`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://api.keywordseverywhere.com/docs/
