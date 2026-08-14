---
name: duckduckgo_search
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `duckduckgo_search`

DuckDuckGo Web Search — privacy-focused web search.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `search`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "duckduckgo_search",
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
| `locale` | string | no |  | Locale code (e.g. 'us-en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "locale": {
      "type": "string",
      "description": "Locale code (e.g. 'us-en')"
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

Top-level keys: `search_metadata`, `search_parameters`, `ads`, `organic_results`, `related_searches`, `pagination`

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
| `search_parameters.locale` | string |  |
| `search_parameters.time_period` | string |  |
| `search_parameters.safe` | string |  |
| `ads[]` | array<object> |  |
| `ads[].position` | integer |  |
| `ads[].title` | string |  |
| `ads[].link` | string |  |
| `ads[].tracking_link` | string |  |
| `ads[].source` | string |  |
| `ads[].snippet` | string |  |
| `ads[].sitelinks[]` | array<object> |  |
| `ads[].favicon` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_Lpb2Z8vDqdsrg2R8JkVgQzRy",
    "status": "Success",
    "created_at": "2026-03-28T20:44:16Z",
    "request_time_taken": 1.88,
    "parsing_time_taken": 0.01,
    "total_time_taken": 1.89,
    "request_url": "https://duckduckgo.com/?t=h_&ia=web&q=instagram.com&kl=us-en&df=a&kp=1",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_Lpb2Z8vDqdsrg2R8JkVgQzRy.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_Lpb2Z8vDqdsrg2
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

- `serpapi_duckduckgo`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
