---
name: youtube_comments
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `youtube_comments`

YouTube Comments — video comments.

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
  "tool_name": "youtube_comments",
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
| `hl` | string | no | `en` | Language code (default 'en') |
| `next_page_token` | string | no |  | Pagination token for the next page of comments |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "video_id": {
      "type": "string",
      "description": "YouTube video ID"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "next_page_token": {
      "type": "string",
      "description": "Pagination token for the next page of comments"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `comments`, `pagination`

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
| `search_parameters.gl` | string |  |
| `search_parameters.hl` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `comments[]` | array<object> |  |
| `comments[].id` | string |  |
| `comments[].link` | string |  |
| `comments[].channel` | object |  |
| `comments[].published_date` | string |  |
| `comments[].text` | string |  |
| `comments[].likes` | integer |  |
| `comments[].replies` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_KMjqpW46ERug3xx1menbZ3LV",
    "status": "Success",
    "created_at": "2026-03-28T21:56:43Z",
    "request_time_taken": 1.81,
    "parsing_time_taken": 0.01,
    "total_time_taken": 1.81,
    "request_url": "https://www.youtube.com/watch?v=2YSB468mn4M",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_KMjqpW46ERug3xx1menbZ3LV.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_KMjqpW46ERug3xx1menbZ3LV"
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

- `youtube_channel`
- `youtube_channel_videos`
- `youtube_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
