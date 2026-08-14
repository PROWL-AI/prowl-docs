---
name: serpapi_google_events
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_events`

Google Events search via SerpAPI — upcoming events by location.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_events",
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
| `location` | string | no |  | Location for geo-targeted results (e.g. 'Austin, Texas') |
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
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'Austin, Texas')"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `events_results`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_events_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.q` | string |  |
| `search_parameters.engine` | string |  |
| `search_parameters.hl` | string |  |
| `search_information` | object |  |
| `search_information.events_results_state` | string |  |
| `events_results[]` | array<object> |  |
| `events_results[].title` | string |  |
| `events_results[].date` | object |  |
| `events_results[].address[]` | array<string> |  |
| `events_results[].link` | string |  |
| `events_results[].event_location_map` | object |  |
| `events_results[].ticket_info[]` | array<object> |  |
| `events_results[].venue` | object |  |
| `events_results[].thumbnail` | string |  |
| `events_results[].image` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d789c23125cbfd6326c",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/EnRL2FuvTMr7PiCSt2n0DQ/69c83d789c23125cbfd6326c.json",
    "created_at": "2026-03-28 20:43:36 UTC",
    "processed_at": "2026-03-28 20:43:36 UTC",
    "google_events_url": "https://www.google.com/search?q=instagram.com&ibp=htl;events&hl=en",
    "raw_html_file": "https://serpapi.com/searches/EnRL2FuvTMr7PiCSt2n0DQ/69c83d789c23125cbfd6326c.html",
    "total_ti
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

## Alternatives

- `google_events`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
