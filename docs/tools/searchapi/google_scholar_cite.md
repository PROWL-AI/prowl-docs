---
name: google_scholar_cite
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_scholar_cite`

Google Scholar Cite — citation formats (APA, MLA, Chicago, etc.) for a paper by data_cid (from google_scholar results).

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
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_scholar_cite",
  "params": {
    "data_cid": "data_cid_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `data_cid` | string | yes |  | Citation ID from Google Scholar search results (data_cid field) |
| `hl` | string | no |  | Language code |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "data_cid": {
      "type": "string",
      "description": "Citation ID from Google Scholar search results (data_cid field)"
    },
    "hl": {
      "type": "string",
      "description": "Language code"
    }
  },
  "required": [
    "data_cid"
  ]
}
```

## Example request

```json
{
  "data_cid": "data_cid_example"
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
  "error": "Missing required parameter data_cid."
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

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'google_scholar', 'extract': '?'}`

## Alternatives

- `google_about_this_domain`
- `google_ads_advertiser_info`
- `google_ads_transparency_advertiser_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
