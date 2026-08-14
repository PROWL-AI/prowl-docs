---
name: tiktok_profile
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `tiktok_profile`

TikTok Profile — user profile info and recent posts.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `searchapi`, `tiktok` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "tiktok_profile",
  "params": {
    "username": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `username` | string | yes |  | TikTok username |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "username": {
      "type": "string",
      "description": "TikTok username"
    }
  },
  "required": [
    "username"
  ]
}
```

## Example request

```json
{
  "username": "example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `profile`

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
| `search_parameters.username` | string |  |
| `profile` | object |  |
| `profile.username` | string |  |
| `profile.name` | string |  |
| `profile.bio` | string |  |
| `profile.avatar` | string |  |
| `profile.avatar_hd` | string |  |
| `profile.is_verified` | boolean |  |
| `profile.is_business` | boolean |  |
| `profile.posts` | integer |  |
| `profile.followers` | integer |  |
| `profile.following` | integer |  |
| `profile.bio_link` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_KMjqpW46ERug3b8bzenbZ3LV",
    "status": "Success",
    "created_at": "2026-03-28T20:44:12Z",
    "request_time_taken": 1.11,
    "parsing_time_taken": 0.01,
    "total_time_taken": 1.12,
    "request_url": "https://www.tiktok.com/@instagram",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_KMjqpW46ERug3b8bzenbZ3LV.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_KMjqpW46ERug3b8bzenbZ3LV"
  },
  "search_parameters
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

- `tiktok_ads_library`
- `tiktok_ads_library_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
