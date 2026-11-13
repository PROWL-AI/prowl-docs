---
name: google_scholar_author
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-11-13T02:31:46Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_scholar_author`

Google Scholar Author — author profile with publications, citations, and h-index.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `searchapi` |
| Last schema check | `PASS` — 2026-11-12T02:56:36Z |
| Last live API check | `PASS` — 2026-11-12T02:56:36.486392 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_scholar_author",
  "params": {
    "author_id": "author_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `author_id` | string | yes |  | Google Scholar author ID |
| `hl` | string | no |  | Language code (e.g. 'en', 'de', 'pt-BR'); defaults to the run's market language |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "author_id": {
      "type": "string",
      "description": "Google Scholar author ID"
    },
    "hl": {
      "type": "string",
      "description": "Language code (e.g. 'en', 'de', 'pt-BR'); defaults to the run's market language",
      "pattern": "^[A-Za-z]{2,3}(?:[-_][A-Za-z0-9]{2,4})?$"
    }
  },
  "required": [
    "author_id"
  ]
}
```

## Example request

```json
{
  "author_id": "author_id_example"
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
| `search_parameters.author_id` | string |  |
| `search_parameters.hl` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_d97LXP4morub2zLgmk03EOrl",
    "status": "Success",
    "created_at": "2026-03-28T20:43:56Z",
    "request_time_taken": 0.67,
    "parsing_time_taken": 0.0,
    "total_time_taken": 0.67,
    "request_url": "https://scholar.google.com/citations?user=instagram.com&hl=en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_d97LXP4morub2zLgmk03EOrl.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_d97LXP4morub2zLgmk03EOrl
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

- `google_about_this_domain`
- `google_ads_transparency_advertiser_search`
- `google_ai_mode`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs/google
