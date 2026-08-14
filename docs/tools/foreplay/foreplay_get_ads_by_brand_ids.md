---
name: foreplay_get_ads_by_brand_ids
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_get_ads_by_brand_ids`

Get ad creatives for one or more brand IDs from Foreplay.

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
  "tool_name": "foreplay_get_ads_by_brand_ids",
  "params": {
    "brand_ids": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `brand_ids` | string[] | yes |  | List of brand IDs to fetch ads for |
| `limit` | integer | no | `30` | Max ads to return |
| `start_date` | string | no |  | Start date (YYYY-MM-DD) |
| `end_date` | string | no |  | End date (YYYY-MM-DD HH:MM:SS) |
| `order` | enum(newest, oldest, longest_running, most_relevant) | no | `newest` | Sort order |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "brand_ids": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of brand IDs to fetch ads for"
    },
    "limit": {
      "type": "integer",
      "description": "Max ads to return",
      "default": 30,
      "minimum": 1,
      "maximum": 250
    },
    "start_date": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD)"
    },
    "end_date": {
      "type": "string",
      "description": "End date (YYYY-MM-DD HH:MM:SS)"
    },
    "order": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "newest",
        "oldest",
        "longest_running",
        "most_relevant"
      ],
      "default": "newest"
    }
  },
  "required": [
    "brand_ids"
  ]
}
```

## Example request

```json
{
  "brand_ids": []
}
```

## Output

Ad creatives with enriched URLs

Key fields: `data[].landing_page_url`, `data[].creative_media_urls`, `data[].facebook_ad_library_url`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use brand IDs from foreplay_get_brands_by_domain or foreplay_discovery_brands

**Chain inputs:** `{'param': 'brand_ids', 'from_tool': 'foreplay_discovery_ads', 'extract': 'data[].brand_id'}`

**Chain groups:** `foreplay`

## Alternatives

_None listed._

## Provider docs

https://docs.foreplay.co
