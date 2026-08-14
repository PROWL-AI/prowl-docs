---
name: tiktok_ads_library
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `tiktok_ads_library`

TikTok Ads Library — search TikTok ads by keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `ads`, `searchapi`, `tiktok` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "tiktok_ads_library",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `query` | string | yes |  | Search query |
| `country` | string | no |  | Country code (e.g. 'US') |
| `time_period` | string | no |  | Date range filter (YYYY-MM-DD..YYYY-MM-DD) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Search query"
    },
    "country": {
      "type": "string",
      "description": "Country code (e.g. 'US')"
    },
    "time_period": {
      "type": "string",
      "description": "Date range filter (YYYY-MM-DD..YYYY-MM-DD)"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `ads`, `pagination`

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
| `search_parameters.country` | string |  |
| `search_parameters.time_period` | string |  |
| `search_parameters.sort_by` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `ads[]` | array<object> |  |
| `ads[].position` | integer |  |
| `ads[].id` | string |  |
| `ads[].advertiser` | string |  |
| `ads[].first_shown_datetime` | string |  |
| `ads[].last_shown_datetime` | string |  |
| `ads[].video_link` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_1r3VbxvXpgtM9YArKvB26gOP",
    "status": "Success",
    "created_at": "2026-03-28T20:44:01Z",
    "request_time_taken": 9.48,
    "parsing_time_taken": 0.0,
    "total_time_taken": 9.48,
    "request_url": "https://library.tiktok.com/ads?region=all&start_time=1743134400000&end_time=1774670400000&sort_type=last_shown_date%2Cdesc&adv_name=instagram.com&adv_biz_ids=&query_type=1",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_1r3VbxvXpgt
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

- Engine-specific SearchAPI surface — pass marketplace/locale params when the schema exposes them
- ID-like params (property_id, asin, place_id) must be real identifiers from a prior search tool

## Alternatives

- `tiktok_ads_library_advertiser_search`
- `google_ads_transparency_advertiser_search`
- `linkedin_ad_library`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
