---
name: serpapi_youtube
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_youtube`

YouTube Search via SerpAPI — video results with metadata.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `serp`, `serpapi`, `serpapi_serp`, `youtube` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_youtube",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `gl` | string | no |  | Country code for results, e.g. 'de' (two-letter ISO). Defaults to the run's market. |
| `hl` | string | no |  | Interface language code, e.g. 'de'. Defaults to the run's market. |
| `q` | string | yes |  | Search query |
| `sp` | string | no |  | Search parameter filter (encoded) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "gl": {
      "type": "string",
      "description": "Country code for results, e.g. 'de' (two-letter ISO). Defaults to the run's market."
    },
    "hl": {
      "type": "string",
      "description": "Interface language code, e.g. 'de'. Defaults to the run's market."
    },
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "sp": {
      "type": "string",
      "description": "Search parameter filter (encoded)"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `video_results`, `ads_results`, `channels_new_to_you`, `people_also_search_for`, `from_related_searches`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.youtube_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.search_query` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `search_information.video_results_state` | string |  |
| `video_results[]` | array<object> |  |
| `video_results[].position_on_page` | integer |  |
| `video_results[].title` | string |  |
| `video_results[].link` | string |  |
| `video_results[].serpapi_link` | string |  |
| `video_results[].video_id` | string |  |
| `video_results[].channel` | object |  |
| `video_results[].published_date` | string |  |
| `video_results[].views` | integer |  |
| `video_results[].length` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8c73d175b558f39260",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/N6cxMcTW0DGkMnW59K2KEQ/69c83d8c73d175b558f39260.json",
    "created_at": "2026-03-28 20:43:56 UTC",
    "processed_at": "2026-03-28 20:43:56 UTC",
    "youtube_url": "https://www.youtube.com/results?search_query=instagram.com",
    "raw_html_file": "https://serpapi.com/searches/N6cxMcTW0DGkMnW59K2KEQ/69c83d8c73d175b558f39260.html",
    "total_time_taken": 1.4
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

**Chain groups:** `serpapi_youtube`

## Alternatives

- `youtube_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
