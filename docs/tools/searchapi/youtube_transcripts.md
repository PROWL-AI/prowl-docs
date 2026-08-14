---
name: youtube_transcripts
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `youtube_transcripts`

YouTube Transcripts — get video transcript/captions by video ID.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `searchapi`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "youtube_transcripts",
  "params": {
    "video_id": "dQw4w9WgXcQ"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `video_id` | string | yes |  | YouTube video ID |
| `lang` | string | no | `en` | Transcript language code (default 'en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "video_id": {
      "type": "string",
      "description": "YouTube video ID"
    },
    "lang": {
      "type": "string",
      "description": "Transcript language code (default 'en')",
      "default": "en"
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

Top-level keys: `search_metadata`, `search_parameters`, `transcripts`, `available_languages`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.request_time_taken` | number |  |
| `search_metadata.parsing_time_taken` | number |  |
| `search_metadata.total_time_taken` | number |  |
| `search_metadata.request_url` | string |  |
| `search_metadata.html_url` | string |  |
| `search_metadata.json_url` | string |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.video_id` | string |  |
| `search_parameters.lang` | string |  |
| `transcripts[]` | array<object> |  |
| `transcripts[].text` | string |  |
| `transcripts[].start` | number |  |
| `transcripts[].duration` | number |  |
| `available_languages[]` | array<object> |  |
| `available_languages[].name` | string |  |
| `available_languages[].lang` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_JBAO2bkaoPuJ200Vx4n7XajE",
    "status": "Success",
    "created_at": "2026-03-28T21:56:36Z",
    "request_time_taken": 6.32,
    "parsing_time_taken": 0.01,
    "total_time_taken": 6.32,
    "request_url": "https://www.youtube.com/watch?v=2YSB468mn4M",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_JBAO2bkaoPuJ200Vx4n7XajE.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_JBAO2bkaoPuJ200Vx4n7XajE"
  },
  "search_
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

- Typical chain: channel/search → videos → transcripts/comments for content intelligence
- Requires SEARCH_API_KEY; quota/cost scales with result depth

**Chain inputs:** `{'param': 'video_id', 'from_tool': 'youtube_search', 'extract': 'videos[].id'}`

**Chain groups:** `searchapi_youtube`

## Alternatives

- `serpapi_youtube_transcript`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
