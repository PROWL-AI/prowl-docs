---
name: meta_ad_library_ad_details
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `meta_ad_library_ad_details`

Meta Ad Library Ad Details — full creative details for a specific Meta ad by ad_archive_id (Library ID).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "meta_ad_library_ad_details",
  "params": {
    "ad_archive_id": "ad_archive_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `ad_archive_id` | string | yes |  | Ad archive ID (Library ID from Meta Ad Library) |
| `ad_details_token` | string | no |  | Convenience token encoding ad_archive_id, page_id, country (from meta_ad_library results) |
| `page_id` | string | no |  | Advertiser's page ID (required when country is specified) |
| `country` | string | no |  | Country for transparency data (requires page_id) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "ad_archive_id": {
      "type": "string",
      "description": "Ad archive ID (Library ID from Meta Ad Library)"
    },
    "ad_details_token": {
      "type": "string",
      "description": "Convenience token encoding ad_archive_id, page_id, country (from meta_ad_library results)"
    },
    "page_id": {
      "type": "string",
      "description": "Advertiser's page ID (required when country is specified)"
    },
    "country": {
      "type": "string",
      "description": "Country for transparency data (requires page_id)"
    }
  },
  "required": [
    "ad_archive_id"
  ]
}
```

## Example request

```json
{
  "ad_archive_id": "ad_archive_id_example"
}
```

## Output

Top-level keys: `error`

| Path | Type | Description |
|------|------|-------------|
| `error` | string |  |

### Example response (from profile)

```json
{
  "error": "Missing required parameter ad_archive_id."
}
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

**Chain inputs:** `{'param': 'ad_id', 'from_tool': 'meta_ad_library', 'extract': 'ads[].ad_archive_id'}`

**Chain groups:** `searchapi_meta`

## Alternatives

- `google_ads_advertiser_info`
- `google_ads_transparency_advertiser_search`
- `linkedin_ad_library`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
