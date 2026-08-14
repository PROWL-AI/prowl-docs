---
name: serpapi_google_finance
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_finance`

Google Finance stock/market data via SerpAPI (ticker symbol like AAPL, GOOGL).

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `finance`, `google`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_finance",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Ticker symbol (e.g. 'AAPL', 'GOOGL') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Ticker symbol (e.g. 'AAPL', 'GOOGL')"
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

Top-level keys: `search_metadata`, `search_parameters`, `markets`, `discover_more`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_finance_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.hl` | string |  |
| `markets` | object |  |
| `markets.us[]` | array<object> |  |
| `markets.europe[]` | array<object> |  |
| `markets.asia[]` | array<object> |  |
| `markets.currencies[]` | array<object> |  |
| `markets.crypto[]` | array<object> |  |
| `markets.futures[]` | array<object> |  |
| `discover_more[]` | array<object> |  |
| `discover_more[].title` | string |  |
| `discover_more[].items[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d7f421b08436e5beedb",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/yr3kDy-AkylR-rW4P3Z8Ng/69c83d7f421b08436e5beedb.json",
    "created_at": "2026-03-28 20:43:43 UTC",
    "processed_at": "2026-03-28 20:43:43 UTC",
    "google_finance_url": "https://www.google.com/finance/quote/instagram.com?hl=en",
    "raw_html_file": "https://serpapi.com/searches/yr3kDy-AkylR-rW4P3Z8Ng/69c83d7f421b08436e5beedb.html",
    "total_time_taken"
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

## Alternatives

- `google_finance`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
