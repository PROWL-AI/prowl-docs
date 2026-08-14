---
name: google_lens
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_lens`

Google Lens — visual search by image URL.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_lens",
  "params": {
    "url": "https://example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `url` | string | yes |  | Image URL to search |
| `hl` | string | no | `en` | Language code (default 'en') |
| `country` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Image URL to search"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "country": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    }
  },
  "required": [
    "url"
  ]
}
```

## Example request

```json
{
  "url": "https://example.com"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `error`

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
| `search_parameters.url` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.search_type` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_G6ZMRV4jp7tBErNB5k2X071E",
    "status": "Success",
    "created_at": "2026-03-28T20:43:50Z",
    "request_time_taken": 5.94,
    "parsing_time_taken": 0.0,
    "total_time_taken": 5.94,
    "request_url": "https://lens.google.com/uploadbyurl?url=https%3A%2F%2Fwww.instagram.com&hl=en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_G6ZMRV4jp7tBErNB5k2X071E.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_G6ZMRV4j
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

- Requires SEARCH_API_KEY; prefer google_*_light variants when you only need titles/links
- Geo via location / gl / hl — set them for market-specific SERPs
- Full google_* engines are richer but costlier than light twins

## Alternatives

- `serpapi_google_lens`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
