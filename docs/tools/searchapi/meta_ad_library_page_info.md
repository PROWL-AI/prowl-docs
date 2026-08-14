---
name: meta_ad_library_page_info
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `meta_ad_library_page_info`

Meta Ad Library Page Info — detailed Facebook page info including name, likes, verification, transparency, Instagram data, and ad spend.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `onpage`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "meta_ad_library_page_info",
  "params": {
    "page_id": "page_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `page_id` | string | yes |  | Facebook page ID |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "page_id": {
      "type": "string",
      "description": "Facebook page ID"
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

Top-level keys: `search_metadata`, `search_parameters`, `page`, `ad_library_page_info`

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
| `page.name` | string |  |
| `page.id` | string |  |
| `page.url` | string |  |
| `page.about` | object |  |
| `page.about.text` | string |  |
| `page.is_delegate_page_with_linked_primary_profile` | boolean |  |
| `page.confirmed_page_owner` | object |  |
| `page.confirmed_page_owner.name` | string |  |
| `page.confirmed_page_owner.information` | object |  |
| `page.confirmed_page_owner.id` | string |  |
| `page.pages_transparency_info` | object |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_DWmO1QkoEbuMGDxXP4J2r8Ga",
    "status": "Success",
    "created_at": "2026-03-28T22:01:44Z",
    "request_time_taken": 3.35,
    "parsing_time_taken": 0.0,
    "total_time_taken": 3.35,
    "request_url": "https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=ALL&search_type=page&view_all_page_id=367152833370567",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_DWmO1QkoEbuMGDxXP4J2r8Ga.html",
    "json_url": "h
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

**Chain inputs:** `{'param': 'page_id', 'from_tool': 'meta_ad_library_page_search', 'extract': 'page_results[].page_id'}`

**Chain groups:** `searchapi_meta`

## Alternatives

- `meta_ad_library_page_search`
- `facebook_business_page`
- `facebook_business_page_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
