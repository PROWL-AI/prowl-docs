---
name: youtube_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `youtube_search`

YouTube Search — search videos by query.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `search`, `searchapi`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "youtube_search",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Search query |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
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
    "q"
  ]
}
```

## Example request

```json
{
  "q": "example query"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `videos`, `people_also_search_for`, `pagination`

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
| `search_parameters.q` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.gl` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `videos[]` | array<object> |  |
| `videos[].position` | integer |  |
| `videos[].id` | string |  |
| `videos[].title` | string |  |
| `videos[].link` | string |  |
| `videos[].description` | string |  |
| `videos[].views` | integer |  |
| `videos[].channel` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_yawpDZvY5RcVxQWXXvWPdXoM",
    "status": "Success",
    "created_at": "2026-03-28T20:44:10Z",
    "request_time_taken": 0.72,
    "parsing_time_taken": 0.01,
    "total_time_taken": 0.73,
    "request_url": "https://www.youtube.com/results?search_query=instagram.com&gl=US&hl=en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_yawpDZvY5RcVxQWXXvWPdXoM.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_yawpDZvY5RcVxQ
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

**Chain groups:** `searchapi_youtube`, `dataforseo_youtube`

## Alternatives

- `serpapi_youtube`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
