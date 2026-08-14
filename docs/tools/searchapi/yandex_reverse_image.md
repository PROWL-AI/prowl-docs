---
name: yandex_reverse_image
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `yandex_reverse_image`

Yandex Reverse Image — search by image URL to find similar images and sources.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "yandex_reverse_image",
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

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "Image URL to search"
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

Top-level keys: `search_metadata`, `search_parameters`, `image_preview`

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
| `image_preview` | object |  |
| `image_preview.image` | object |  |
| `image_preview.image.width` | integer |  |
| `image_preview.image.height` | integer |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_dXG2jzvrlqTobaAXdeYoaOb8",
    "status": "Success",
    "created_at": "2026-03-28T20:44:20Z",
    "request_time_taken": 2.39,
    "parsing_time_taken": 0.0,
    "total_time_taken": 2.39,
    "request_url": "https://yandex.com/images/search/?url=https://www.instagram.com&rpt=imageview",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_dXG2jzvrlqTobaAXdeYoaOb8.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_dXG2jzvr
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

## Alternatives

_None listed._

## Provider docs

https://www.searchapi.io/docs
