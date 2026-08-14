---
name: serpapi_youtube_transcript
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_youtube_transcript`

YouTube video transcript via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `serp`, `serpapi`, `serpapi_serp`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_youtube_transcript",
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
| `lang` | string | no |  | Transcript language code |

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
      "description": "Transcript language code"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `error`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.youtube_video_transcript_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.v` | string |  |
| `search_parameters.language_code` | string |  |
| `search_information` | object |  |
| `search_information.results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c850238c8a7e28a1d83212",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/29Qo2PmLbWaLNK6oq7CZ8Q/69c850238c8a7e28a1d83212.json",
    "created_at": "2026-03-28 22:03:15 UTC",
    "processed_at": "2026-03-28 22:03:15 UTC",
    "youtube_video_transcript_url": "https://www.youtube.com/watch?v=b2HNVEP4vig",
    "raw_html_file": "https://serpapi.com/searches/29Qo2PmLbWaLNK6oq7CZ8Q/69c850238c8a7e28a1d83212.html",
    "prettify_html_file":
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SERP_API_KEY | Check SERP_API_KEY in .env or SerpAPI dashboard |
| 429 | Monthly rate limit reached | Upgrade SerpAPI plan or wait for quota reset |
| 400 | Missing required parameters | Check query and engine parameters |

## When to use

- SerpAPI engine is encoded in the tool name — do not re-pass engine unless the schema requires it
- Prefer the SearchAPI twin when cost/coverage is better for the same surface
- Paginate with num/start (or page) when result sets are truncated

**Chain inputs:** `{'param': 'video_id', 'from_tool': 'serpapi_youtube', 'extract': 'video_results[].link'}`

**Chain groups:** `serpapi_youtube`

## Alternatives

- `youtube_transcripts`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
