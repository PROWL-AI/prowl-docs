---
name: google_ads_advertiser_info
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_ads_advertiser_info`

Google Ads Advertiser Info — get details about an advertiser by their advertiser_info_token (obtained from Google Search ad results).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_ads_advertiser_info",
  "params": {
    "advertiser_info_token": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `advertiser_info_token` | string | yes |  | Token identifying the advertiser (from Google Search ad results) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "advertiser_info_token": {
      "type": "string",
      "description": "Token identifying the advertiser (from Google Search ad results)"
    }
  },
  "required": [
    "advertiser_info_token"
  ]
}
```

## Example request

```json
{
  "advertiser_info_token": "example"
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
  "error": "Missing required parameter advertiser_info_token."
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

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

**Chain inputs:** `{'param': 'advertiser_id', 'from_tool': 'google_ads_transparency_advertiser_search', 'extract': 'advertisers[].id'}`

**Chain groups:** `searchapi_ads_transparency`

## Alternatives

- `google_ads_transparency_advertiser_search`
- `dataforseo_kw_google_ads_ad_traffic`
- `dataforseo_kw_google_ads_keywords_for_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
