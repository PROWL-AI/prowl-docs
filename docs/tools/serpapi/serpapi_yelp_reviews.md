---
name: serpapi_yelp_reviews
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_yelp_reviews`

Yelp business reviews via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `reviews`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_yelp_reviews",
  "params": {
    "place_id": "ChIJj61dQgK6j4AR4GeTYWZsKWw"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `place_id` | string | yes |  | Yelp place_id from search results |
| `start` | integer | no |  | Review offset for pagination |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "place_id": {
      "type": "string",
      "description": "Yelp place_id from search results"
    },
    "start": {
      "type": "integer",
      "description": "Review offset for pagination"
    }
  },
  "required": [
    "place_id"
  ]
}
```

## Example request

```json
{
  "place_id": "ChIJj61dQgK6j4AR4GeTYWZsKWw"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `error`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.yelp_reviews_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.start` | integer |  |
| `search_parameters.num` | string |  |
| `search_parameters.place_id` | string |  |
| `search_information` | object |  |
| `search_information.reviews_results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d8f2c2bb4e4ea6d5d3b",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/brUzxuxQDyKTmqMK48KZyg/69c83d8f2c2bb4e4ea6d5d3b.json",
    "created_at": "2026-03-28 20:43:59 UTC",
    "processed_at": "2026-03-28 20:43:59 UTC",
    "yelp_reviews_url": "https://www.yelp.com/biz/instagram.com",
    "raw_html_file": "https://serpapi.com/searches/brUzxuxQDyKTmqMK48KZyg/69c83d8f2c2bb4e4ea6d5d3b.html",
    "prettify_html_file": "https://serpapi
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SERP_API_KEY | Check SERP_API_KEY in .env or SerpAPI dashboard |
| 429 | Monthly rate limit reached | Upgrade SerpAPI plan or wait for quota reset |
| 400 | Missing required parameters | Check query and engine parameters |

## When to use

- SerpAPI engine is encoded in the tool name — do not re-pass engine unless the schema requires it
- Prefer the SearchAPI twin when cost/coverage is better for the same surface
- Paginate with num/start (or page) when result sets are truncated

**Chain inputs:** `{'param': '<from_template>', 'from_tool': 'serpapi_yelp', 'extract': '?'}`

## Alternatives

- `serpapi_amazon_reviews`
- `serpapi_apple_reviews`
- `serpapi_google_maps_reviews`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
