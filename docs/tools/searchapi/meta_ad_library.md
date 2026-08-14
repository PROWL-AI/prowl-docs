---
name: meta_ad_library
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `meta_ad_library`

Meta Ad Library — search Facebook/Instagram ads by keyword or advertiser.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `ads`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "meta_ad_library",
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
| `ad_type` | enum(all, political_and_issue_ads) | no |  | Ad type filter |
| `country` | string | no |  | Country code |
| `ad_reached_countries` | string | no |  | Countries the ad reached |
| `media_type` | enum(all, image, video, meme) | no |  | Media type filter |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Search query"
    },
    "ad_type": {
      "type": "string",
      "description": "Ad type filter",
      "enum": [
        "all",
        "political_and_issue_ads"
      ]
    },
    "country": {
      "type": "string",
      "description": "Country code"
    },
    "ad_reached_countries": {
      "type": "string",
      "description": "Countries the ad reached"
    },
    "media_type": {
      "type": "string",
      "description": "Media type filter",
      "enum": [
        "all",
        "image",
        "video",
        "meme"
      ]
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
| `search_parameters.ad_type` | string |  |
| `search_parameters.country` | string |  |
| `search_parameters.media_type` | string |  |
| `search_parameters.sort_by` | string |  |
| `search_information` | object |  |
| `search_information.total_results` | integer |  |
| `ads[]` | array<object> |  |
| `ads[].ad_archive_id` | string |  |
| `ads[].page_id` | string |  |
| `ads[].snapshot` | object |  |
| `ads[].is_active` | boolean |  |
| `ads[].has_user_reported` | boolean |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_Z18NJlvnOYIA3rmPGk3BOm7g",
    "status": "Success",
    "created_at": "2026-03-28T20:43:59Z",
    "request_time_taken": 3.45,
    "parsing_time_taken": 0.05,
    "total_time_taken": 3.5,
    "request_url": "https://www.facebook.com/ads/library/?ad_type=all&active_status=active&country=ALL&media_type=all&is_targeted_country=false&search_type=keyword_unordered&q=instagram.com&sort_data[mode]=total_impressions&sort_data[direction]=desc",
    "html_url": "h
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

**Chain groups:** `searchapi_meta`

## Alternatives

- `google_ads_transparency_advertiser_search`
- `linkedin_ad_library`
- `meta_ad_library_page_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
