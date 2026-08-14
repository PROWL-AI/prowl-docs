---
name: google_news_portal
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_news_portal`

Google News Portal — organized news sections and topics from Google News.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_news_portal",
  "params": {
    "topic_token": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `topic_token` | string | yes |  | Topic token from Google News results |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "topic_token": {
      "type": "string",
      "description": "Topic token from Google News results"
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
    "topic_token"
  ]
}
```

## Example request

```json
{
  "topic_token": "example"
}
```

## Output

Google News Portal — organized news sections and topics from Google News.

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

- Chain dependency: obtain `topic_token` from `google_news` first, then pass it here.
- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

**Chain inputs:** `{'param': 'topic_token', 'from_tool': 'google_news', 'extract': '_custom_news_topic_token'}`

**Chain groups:** `searchapi_news`

## Alternatives

- `google_about_this_domain`
- `google_ads_advertiser_info`
- `google_ads_transparency_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
