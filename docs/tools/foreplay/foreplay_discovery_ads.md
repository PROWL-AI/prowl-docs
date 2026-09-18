---
name: foreplay_discovery_ads
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-09-18T15:14:52Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_discovery_ads`

Search and discover ads across platforms (Facebook, Instagram, TikTok, YouTube, LinkedIn) using Foreplay.

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
  "tool_name": "foreplay_discovery_ads",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Search query for ads (e.g. brand name, product, keyword) |
| `limit` | integer | no | `10` | Max results |
| `start_date` | string | no |  | Start date filter (YYYY-MM-DD HH:MM:SS) |
| `end_date` | string | no |  | End date filter (YYYY-MM-DD HH:MM:SS) |
| `live` | boolean | no |  | Filter for currently active ads only |
| `display_formats` | string[] | no |  | Filter by ad display formats |
| `publisher_platforms` | string[] | no |  | Filter by publisher platforms |
| `niches` | string[] | no |  | Filter by business niches |
| `order` | enum(newest, oldest, longest_running, most_relevant) | no | `newest` | Sort order |
| `market_targets` | string[] | no |  | Filter by who the ad sells to — the cheapest way to keep B2C creatives out of a B2B search. |
| `languages` | string[] | no |  | Filter by ad language, as two-letter codes (e.g. ['en', 'de']). |
| `video_duration_min` | integer | no |  | Only videos at least this many seconds long. |
| `video_duration_max` | integer | no |  | Only videos at most this many seconds long. |
| `running_duration_min_days` | integer | no |  | Only ads that have been running at least this many days — an ad alive for months is a proven one. |
| `running_duration_max_days` | integer | no |  | Only ads running no longer than this many days. |
| `cursor` | string | no |  | Page token from a previous response's `metadata.cursor`. Without it only the first page is reachable. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Search query for ads (e.g. brand name, product, keyword)"
    },
    "limit": {
      "type": "integer",
      "description": "Max results",
      "default": 10,
      "minimum": 1,
      "maximum": 250
    },
    "start_date": {
      "type": "string",
      "description": "Start date filter (YYYY-MM-DD HH:MM:SS)"
    },
    "end_date": {
      "type": "string",
      "description": "End date filter (YYYY-MM-DD HH:MM:SS)"
    },
    "live": {
      "type": "boolean",
      "description": "Filter for currently active ads only"
    },
    "display_formats": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "carousel",
          "dco",
          "dpa",
          "event",
          "image",
          "multi_images",
          "multi_medias",
          "multi_videos",
          "page_like",
          "text",
          "video"
        ]
      },
      "description": "Filter by ad display formats"
    },
    "publisher_platforms": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "facebook",
          "instagram",
          "audience_network",
          "messenger",
          "tiktok",
          "youtube",
          "linkedin",
          "threads"
        ]
      },
      "description": "Filter by publisher platforms"
    },
    "niches": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "accessories",
          "app/software",
          "beauty",
          "business/professional",
          "education",
          "entertainment",
          "fashion",
          "food/drink",
          "health/wellness",
          "home/garden",
          "jewelry/watches",
          "parenting",
          "pets",
          "real estate",
          "service business",
          "other"
        ]
      },
      "description": "Filter by business niches"
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
    },
    "market_targets": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "b2b",
          "b2c"
        ]
      },
      "description": "Filter by who the ad sells to \u2014 the cheapest way to keep B2C creatives out of a B2B search."
    },
    "languages": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Filter by ad language, as two-letter codes (e.g. ['en', 'de'])."
    },
    "video_duration_min": {
      "type": "integer",
      "description": "Only videos at least this many seconds long.",
      "minimum": 0
    },
    "video_duration_max": {
      "type": "integer",
      "description": "Only videos at most this many seconds long.",
      "minimum": 1
    },
    "running_duration_min_days": {
      "type": "integer",
      "description": "Only ads that have been running at least this many days \u2014 an ad alive for months is a proven one.",
      "minimum": 0
    },
    "running_duration_max_days": {
      "type": "integer",
      "description": "Only ads running no longer than this many days.",
      "minimum": 1
    },
    "cursor": {
      "type": "string",
      "description": "Page token from a previous response's `metadata.cursor`. Without it only the first page is reachable."
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

Paginated ads response with enriched URLs

Key fields: `data[].landing_page_url`, `data[].creative_media_urls`, `data[].facebook_ad_library_url`, `data[].creative_preview_url`, `_url_summary`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use `order=longest_running` to find proven ad winners
- Combine with foreplay_get_brands_by_domain for domain-specific ad discovery
- Formats: carousel, dco, dpa, event, image, multi_images, multi_videos, video, text
- Platforms: facebook, instagram, tiktok, youtube, linkedin, messenger, threads

**Chain groups:** `foreplay`

## Alternatives

- `foreplay_get_brands_by_domain`
- `foreplay_discovery_brands`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.foreplay.co
