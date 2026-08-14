---
name: google_hotels_property
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_hotels_property`

Google Hotels Property — detailed hotel info with room types, pricing across booking sites, and reviews.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_hotels_property",
  "params": {
    "check_in_date": "YYYY-MM-DD",
    "check_out_date": "YYYY-MM-DD",
    "property_token": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `property_token` | string | yes |  | Property token from google_hotels results |
| `check_in_date` | string | yes |  | Check-in date (YYYY-MM-DD) — required by the engine |
| `check_out_date` | string | yes |  | Check-out date (YYYY-MM-DD) — required by the engine |
| `hl` | string | no |  | Language code |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "property_token": {
      "type": "string",
      "description": "Property token from google_hotels results"
    },
    "check_in_date": {
      "type": "string",
      "description": "Check-in date (YYYY-MM-DD) \u2014 required by the engine"
    },
    "check_out_date": {
      "type": "string",
      "description": "Check-out date (YYYY-MM-DD) \u2014 required by the engine"
    },
    "hl": {
      "type": "string",
      "description": "Language code"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    },
    "currency": {
      "type": "string",
      "description": "Currency code (e.g. 'USD', 'EUR')"
    }
  },
  "required": [
    "property_token",
    "check_in_date",
    "check_out_date"
  ]
}
```

## Example request

```json
{
  "check_in_date": "YYYY-MM-DD",
  "check_out_date": "YYYY-MM-DD",
  "property_token": "example"
}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Unsupported value `en` in hl parameter."
}
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SEARCH_API_KEY | Skip SearchAPI tools — use Exa or Perplexity as alternatives for web search |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 422 | Invalid parameters | Check query and filter parameters match the expected format |

## When to use

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

## Alternatives

- `google_about_this_domain`
- `google_ads_transparency_advertiser_search`
- `google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
