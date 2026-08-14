---
name: google_shopping_filters
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_shopping_filters`

Google Shopping Filters — complete list of filter options for Shopping results.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `searchapi`, `shopping` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_shopping_filters",
  "params": {
    "all_filters_token": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `all_filters_token` | string | yes |  | All filters token from google_shopping results |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "all_filters_token": {
      "type": "string",
      "description": "All filters token from google_shopping results"
    }
  },
  "required": [
    "all_filters_token"
  ]
}
```

## Example request

```json
{
  "all_filters_token": "example"
}
```

## Output

Google Shopping Filters — complete list of filter options for Shopping results.

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

- Chain dependency: obtain `all_filters_token` from `google_shopping` first, then pass it here.
- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

**Chain inputs:** `{'param': 'all_filters_token', 'from_tool': 'google_shopping', 'extract': '_custom_shopping_filters_token'}`

**Chain groups:** `searchapi_shopping`

## Alternatives

- `google_shopping`
- `google_shopping_autocomplete`
- `serpapi_google_shopping`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
