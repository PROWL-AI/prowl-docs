---
name: dataforseo_serp_youtube_video_subtitles
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_youtube_video_subtitles`

Extract YouTube video subtitles/captions — get full transcript text for content analysis.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `serp`, `video`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_youtube_video_subtitles",
  "params": {
    "video_id": "dQw4w9WgXcQ"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `device` | enum(desktop) | no |  | device type |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `os` | string | no |  | device operating system |
| `subtitles_translate_language` | string | no |  | language code of translated text |
| `tag` | string | no |  | user-defined task identifier |
| `video_id` | string | yes |  | YouTube video ID |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |
| `subtitles_language` | string | no |  | Subtitles language code (e.g. 'en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "device": {
      "type": "string",
      "description": "device type",
      "enum": [
        "desktop"
      ]
    },
    "language_code": {
      "type": "string",
      "description": "search engine language code"
    },
    "location_code": {
      "type": "integer",
      "description": "search engine location code"
    },
    "os": {
      "type": "string",
      "description": "device operating system"
    },
    "subtitles_translate_language": {
      "type": "string",
      "description": "language code of translated text"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "video_id": {
      "type": "string",
      "description": "YouTube video ID"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    },
    "subtitles_language": {
      "type": "string",
      "description": "Subtitles language code (e.g. 'en')"
    }
  },
  "required": [
    "video_id"
  ]
}
```

## Example request

```json
{
  "video_id": "dQw4w9WgXcQ"
}
```

## Output

Top-level keys: `version`, `status_code`, `status_message`, `time`, `cost`, `tasks_count`, `tasks_error`, `tasks`

| Path | Type | Description |
|------|------|-------------|
| `tasks[].result[]` | array<object> |  |
| `tasks[].result[].keyword` | string |  |
| `tasks[].result[].items[]` | array<object> |  |

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

- Extract full subtitle/caption text from YouTube videos for competitor messaging analysis.

## Alternatives

- `dataforseo_serp_youtube_organic`
- `serpapi_bing_videos`
- `serpapi_google_videos`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
