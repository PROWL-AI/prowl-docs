---
name: youtube_channel
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `youtube_channel`

YouTube Channel — channel details, subscriber count, and recent videos.

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
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "youtube_channel",
  "params": {
    "channel_id": "UC_x5XG1OV2PQcQyhYqrQ-A"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `channel_id` | string | yes |  | YouTube channel ID |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "channel_id": {
      "type": "string",
      "description": "YouTube channel ID"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    }
  },
  "required": [
    "channel_id"
  ]
}
```

## Example request

```json
{
  "channel_id": "UC_x5XG1OV2PQcQyhYqrQ-A"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `about`, `channel`, `highlighted_video`, `other_channels`, `videos_sections`, `shorts_sections`

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
| `search_parameters.channel_id` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `about` | object |  |
| `about.description` | string |  |
| `about.subscribers` | integer |  |
| `about.videos` | integer |  |
| `about.views` | integer |  |
| `about.joined_date` | string |  |
| `about.joined_date_text` | string |  |
| `about.country` | string |  |
| `about.links[]` | array<object> |  |
| `channel` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_Lpb2Z8vDqdsrg77LdkVgQzRy",
    "status": "Success",
    "created_at": "2026-03-28T21:56:45Z",
    "request_time_taken": 1.48,
    "parsing_time_taken": 0.04,
    "total_time_taken": 1.52,
    "request_url": "https://www.youtube.com/channel/UCdtwPYK_0LG3ll1Op0iAMkQ",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_Lpb2Z8vDqdsrg77LdkVgQzRy.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_Lpb2Z8vDqdsrg77LdkVgQzRy"
  
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

**Chain inputs:** `{'param': 'channel_id', 'from_tool': 'youtube_search', 'extract': 'videos[].channel.id'}`

**Chain groups:** `searchapi_youtube`

## Alternatives

- `youtube_channel_videos`
- `youtube_comments`
- `youtube_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
