---
name: google_travel_explore
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_travel_explore`

Google Travel Explore — discover travel destinations with estimated prices from a departure city.

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
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_travel_explore",
  "params": {
    "departure_id": "departure_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `departure_id` | string | yes |  | Departure city/airport code |
| `hl` | string | no | `en-US` | Locale code (e.g. 'en-US', 'de') — note: bare 'en' is not supported |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "departure_id": {
      "type": "string",
      "description": "Departure city/airport code"
    },
    "hl": {
      "type": "string",
      "description": "Locale code (e.g. 'en-US', 'de') \u2014 note: bare 'en' is not supported",
      "default": "en-US"
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
    "departure_id"
  ]
}
```

## Example request

```json
{
  "departure_id": "departure_id_example"
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
  "error": "Unsupported value `en` in hl parameter. Supported values are `af`, `bs`, `ca`, `cs`, `da`, `de`, `et`, `en-GB`, `en-US`, `es`, `es-419`, `eu`, `fil`, `fr`, `gl`, `hr`, `id`, `is`, `it`, `sw`, `lv`, `lt`, `hu`, `ms`, `nl`, `no`, `pl`, `pt-BR`, `pt-PT`, `ro`, `sq`, `sk`, `sl`, `sr-Latn`, `fi`, `sv`, `vi`, `tr`, `el`, `bg`, `mk`, `mn`, `ru`, `sr`, `uk`, `ka`, `iw`, `ur`, `ar`, `fa`, `am`, `ne`, `mr`, `hi`, `bn`, `pa`, `gu`, `ta`, `te`, `kn`, `ml`, `si`, `th`, `lo`, `km`, `ko`, `ja`, `
...
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
