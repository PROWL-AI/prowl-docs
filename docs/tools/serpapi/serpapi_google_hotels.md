---
name: serpapi_google_hotels
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_hotels`

Google Hotels search via SerpAPI — hotel prices and availability.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_hotels",
  "params": {
    "check_in_date": "YYYY-MM-DD",
    "check_out_date": "YYYY-MM-DD",
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `q` | string | yes |  | Search query |
| `check_in_date` | string | yes |  | Check-in date (YYYY-MM-DD) |
| `check_out_date` | string | yes |  | Check-out date (YYYY-MM-DD) |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `currency` | string | no |  | Currency code (e.g. 'USD', 'EUR') |
| `adults` | integer | no |  | Number of adults |
| `sort_by` | enum(lowest_price, highest_rating, most_reviewed) | no |  | Sort order |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "check_in_date": {
      "type": "string",
      "description": "Check-in date (YYYY-MM-DD)"
    },
    "check_out_date": {
      "type": "string",
      "description": "Check-out date (YYYY-MM-DD)"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    },
    "gl": {
      "type": "string",
      "description": "Country code (e.g. 'us', 'gb')"
    },
    "currency": {
      "type": "string",
      "description": "Currency code (e.g. 'USD', 'EUR')"
    },
    "adults": {
      "type": "integer",
      "description": "Number of adults",
      "minimum": 1,
      "maximum": 9
    },
    "sort_by": {
      "type": "string",
      "description": "Sort order",
      "enum": [
        "lowest_price",
        "highest_rating",
        "most_reviewed"
      ]
    }
  },
  "required": [
    "q",
    "check_in_date",
    "check_out_date"
  ]
}
```

## Example request

```json
{
  "check_in_date": "YYYY-MM-DD",
  "check_out_date": "YYYY-MM-DD",
  "q": "example query"
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
| `search_metadata.google_hotels_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | object |  |
| `search_metadata.total_time_taken.float` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.gl` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.currency` | string |  |
| `search_parameters.check_in_date` | string |  |
| `search_parameters.check_out_date` | string |  |
| `search_parameters.adults` | integer |  |
| `search_parameters.children` | integer |  |
| `search_information` | object |  |
| `search_information.hotels_results_state` | string |  |
| `error` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d83304eba8f6b2953e2",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/scFIRiDPP0NvTKjRtZaJyA/69c83d83304eba8f6b2953e2.json",
    "created_at": "2026-03-28T20:43:47.564Z",
    "processed_at": "2026-03-28T20:43:47.565Z",
    "google_hotels_url": "https://www.google.com/_/TravelFrontendUi/data/batchexecute?rpcids=AtySUc&source-path=/travel/search&hl=en&gl=us&rt=c&soc-app=162&soc-platform=1&soc-device=1",
    "raw_html_file": "http
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

- `google_hotels`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
