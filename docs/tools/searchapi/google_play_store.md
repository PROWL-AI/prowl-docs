---
name: google_play_store
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_play_store`

Google Play Store — search Android apps by name or keyword.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_play_store",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Search query |
| `store` | enum(apps, games) | no | `apps` | Store type |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "store": {
      "type": "string",
      "description": "Store type",
      "enum": [
        "apps",
        "games"
      ],
      "default": "apps"
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
    "q"
  ]
}
```

## Example request

```json
{
  "q": "example query"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `organic_results`

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
| `search_parameters.store` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.hl` | string |  |
| `organic_results[]` | array<object> |  |
| `organic_results[].items[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_rpB8WlvR38SPJ0BLBkXOyEn1",
    "status": "Success",
    "created_at": "2026-03-28T20:44:08Z",
    "request_time_taken": 1.14,
    "parsing_time_taken": 0.01,
    "total_time_taken": 1.15,
    "request_url": "https://play.google.com/store/search?q=instagram.com&hl=en&gl=us&c=apps",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_rpB8WlvR38SPJ0BLBkXOyEn1.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_rpB8WlvR38SPJ
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

**Chain groups:** `searchapi_appstores`, `dataforseo_labs_appstore`

## Alternatives

- `serpapi_google_play`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
