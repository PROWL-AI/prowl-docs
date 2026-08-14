---
name: facebook_business_page
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `facebook_business_page`

Facebook Business Page — page info, posts, and engagement metrics.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `facebook`, `onpage`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "facebook_business_page",
  "params": {
    "page_id": "page_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `page_id` | string | yes |  | Facebook page ID or handle |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "page_id": {
      "type": "string",
      "description": "Facebook page ID or handle"
    }
  },
  "required": [
    "page_id"
  ]
}
```

## Example request

```json
{
  "page_id": "page_id_example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `page`, `about`

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
| `search_parameters.page_id` | string |  |
| `page` | object |  |
| `page.id` | string |  |
| `page.name` | string |  |
| `page.link` | string |  |
| `page.is_verified` | boolean |  |
| `page.followers` | object |  |
| `page.followers.text` | string |  |
| `page.followers.link` | string |  |
| `page.followers.count` | integer |  |
| `page.following` | object |  |
| `page.following.text` | string |  |
| `page.following.link` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_m3WR9zk90VH25wrAMvyn8YoV",
    "status": "Success",
    "created_at": "2026-03-28T22:01:48Z",
    "request_time_taken": 7.73,
    "parsing_time_taken": 0.17,
    "total_time_taken": 7.9,
    "request_url": "https://www.facebook.com/profile.php?id=367152833370567&sk=about",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_m3WR9zk90VH25wrAMvyn8YoV.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_m3WR9zk90VH25wrAMvyn8
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

- SearchAPI.io engine tool — set locale/geo params when available for market-correct results
- Use a prior search/list tool to obtain IDs before detail/reviews calls

**Chain inputs:** `{'param': 'page_id', 'from_tool': 'meta_ad_library_page_search', 'extract': 'page_results[].page_id'}`

**Chain groups:** `searchapi_meta`

## Alternatives

- `dataforseo_biz_social_facebook`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
