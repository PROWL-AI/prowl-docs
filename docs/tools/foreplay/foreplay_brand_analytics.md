---
name: foreplay_brand_analytics
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_brand_analytics`

Get analytics data for a specific brand or page over a date range.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `foreplay` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_brand_analytics",
  "params": {
    "brand_id": "brand_example_001"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `brand_id` | string | yes |  | Brand ID or page ID to analyze |
| `start_date` | string | no |  | Start date (YYYY-MM-DD HH:MM:SS) |
| `end_date` | string | no |  | End date (YYYY-MM-DD HH:MM:SS) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "brand_id": {
      "type": "string",
      "description": "Brand ID or page ID to analyze"
    },
    "start_date": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD HH:MM:SS)"
    },
    "end_date": {
      "type": "string",
      "description": "End date (YYYY-MM-DD HH:MM:SS)"
    }
  },
  "required": [
    "brand_id"
  ]
}
```

## Example request

```json
{
  "brand_id": "brand_example_001"
}
```

## Output

Advertising activity metrics and trends for the brand

Key fields: `metrics`, `trends`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Date format: 'YYYY-MM-DD HH:MM:SS'

**Chain inputs:** `{'param': 'brand_id', 'from_tool': 'foreplay_discovery_ads', 'extract': 'data[].brand_id'}`

**Chain groups:** `foreplay`

## Alternatives

_None listed._

## Provider docs

https://docs.foreplay.co
