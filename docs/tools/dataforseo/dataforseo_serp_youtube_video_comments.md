---
name: dataforseo_serp_youtube_video_comments
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_youtube_video_comments`

Get top 20 YouTube video comments with author info and metrics.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `dataforseo`, `serp`, `video`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_youtube_video_comments",
  "params": {
    "video_id": "dQw4w9WgXcQ"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `depth` | integer | no |  | parsing depth |
| `device` | enum(desktop) | no |  | device type |
| `language_code` | string | no |  | search engine language code |
| `location_code` | integer | no |  | search engine location code |
| `os` | string | no |  | device operating system |
| `tag` | string | no |  | user-defined task identifier |
| `video_id` | string | yes |  | YouTube video ID |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "depth": {
      "type": "integer",
      "description": "parsing depth"
    },
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
| `version` | string |  |
| `status_code` | integer |  |
| `status_message` | string |  |
| `time` | string |  |
| `cost` | integer |  |
| `tasks_count` | integer |  |
| `tasks_error` | integer |  |
| `tasks[]` | array<object> |  |
| `tasks[].id` | string |  |
| `tasks[].status_code` | integer |  |
| `tasks[].status_message` | string |  |
| `tasks[].time` | string |  |
| `tasks[].cost` | integer |  |
| `tasks[].result_count` | integer |  |
| `tasks[].path[]` | array<string> |  |
| `tasks[].data` | object |  |
| `tasks[].result` | null |  |

### Example response (from profile)

```json
{
  "version": "0.1.20260327",
  "status_code": 20000,
  "status_message": "Ok.",
  "time": "0.0113 sec.",
  "cost": 0,
  "tasks_count": 1,
  "tasks_error": 1,
  "tasks": [
    {
      "id": "03282355-1544-0139-0000-3284f105e8e9",
      "status_code": 40501,
      "status_message": "Invalid Field: 'language_name'.",
      "time": "0 sec.",
      "cost": 0,
      "result_count": 0,
      "path": [
        "v3",
        "serp",
        "youtube",
        "video_comments",
        "live",
        "
...
```

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

**Chain inputs:** `{'param': 'video_id', 'from_tool': 'youtube_search', 'extract': 'videos[].id'}`

**Chain groups:** `dataforseo_youtube`

## Alternatives

- `dataforseo_serp_youtube_video_info`
- `dataforseo_serp_youtube_video_subtitles`
- `serpapi_youtube_video`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
