---
name: foreplay_spyder_ads
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_spyder_ads`

Get ads from brands you are tracking via Foreplay Spyder.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `foreplay` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_spyder_ads",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `offset` | integer | no | `0` | Pagination offset (default: 0) |
| `limit` | integer | no | `10` | Max ads |
| `order` | enum(newest, oldest, longest_running) | no | `newest` | Sort order |
| `live` | boolean | no |  | Filter for currently active ads only |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "offset": {
      "type": "integer",
      "description": "Pagination offset (default: 0)",
      "default": 0
    },
    "limit": {
      "type": "integer",
      "description": "Max ads",
      "default": 10,
      "minimum": 1,
      "maximum": 250
    },
    "order": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "newest",
        "oldest",
        "longest_running"
      ],
      "default": "newest"
    },
    "live": {
      "type": "boolean",
      "description": "Filter for currently active ads only"
    }
  },
  "required": []
}
```

## Example request

```json
{}
```

## Output

Ads from tracked brands with enriched URLs

Key fields: `data[].landing_page_url`, `data[].creative_media_urls`, `data[].facebook_ad_library_url`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use to monitor competitor advertising activity in real time

## Alternatives

_None listed._

## Provider docs

https://docs.foreplay.co
