---
name: foreplay_discovery_brands
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_discovery_brands`

Search for brands by name using fuzzy matching via Foreplay.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `foreplay` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_discovery_brands",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Brand name to search for (e.g. 'Airalo') |
| `limit` | integer | no | `10` | Max results (1-10) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Brand name to search for (e.g. 'Airalo')"
    },
    "limit": {
      "type": "integer",
      "description": "Max results (1-10)",
      "default": 10,
      "minimum": 1,
      "maximum": 10
    }
  },
  "required": [
    "query"
  ]
}
```

## Example request

```json
{
  "query": "example query"
}
```

## Output

Brands with enriched URLs

Key fields: `data[].id`, `data[].name`, `data[].facebook_page_url`, `data[].ad_library_url`, `data[].brand_websites`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use returned brand IDs with foreplay_get_ads_by_brand_ids to fetch ad creatives

## Alternatives

- `foreplay_get_brands_by_domain`
- `foreplay_discovery_ads`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.foreplay.co
