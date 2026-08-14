---
name: foreplay_get_ads_by_page_id
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_get_ads_by_page_id`

Get ads for a specific Facebook page ID via Foreplay.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `foreplay`, `onpage` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_get_ads_by_page_id",
  "params": {
    "page_id": "page_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `page_id` | string | yes |  | Facebook page ID or page username |
| `limit` | integer | no | `30` | Max ads |
| `order` | enum(newest, oldest, longest_running, most_relevant) | no | `newest` | Sort order |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "page_id": {
      "type": "string",
      "description": "Facebook page ID or page username"
    },
    "limit": {
      "type": "integer",
      "description": "Max ads",
      "default": 30,
      "minimum": 1,
      "maximum": 250
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
    "page_id"
  ]
}
```

## Example request

```json
{
  "page_id": "page_id_example"
}
```

## Output

Ad creatives with enriched URLs (same as foreplay_get_ads_by_brand_ids)

Key fields: `data[].landing_page_url`, `data[].creative_media_urls`, `data[].facebook_ad_library_url`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Alternative to foreplay_get_ads_by_brand_ids — use when you have a Facebook page ID
- Returns same enriched ad data with landing_page_url, creative_media_urls, etc.

**Chain inputs:** `{'param': 'page_id', 'from_tool': 'foreplay_get_brands_by_domain', 'extract': 'data[].ad_library_id'}`

**Chain groups:** `foreplay`

## Alternatives

- `firecrawl_scrape_page_html`
- `firecrawl_scrape_page_markdown`
- `firecrawl_scrape_page_seo`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.foreplay.co
