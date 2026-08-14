---
name: serpapi_google_trends
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_trends`

Google Trends data via SerpAPI — interest over time and by region.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `google`, `serp`, `serpapi`, `serpapi_serp`, `trends` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_trends",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `data_type` | enum(TIMESERIES, GEO_MAP, GEO_MAP_0, RELATED_TOPICS, RELATED_QUERIES) | no |  | What Trends returns (default: TIMESERIES). RELATED_QUERIES/RELATED_TOPICS and the GEO_MAP breakdowns are unreachable without it. |
| `region` | enum(COUNTRY, REGION, DMA, CITY) | no |  | Geographic granularity for the GEO_MAP data types. |
| `cat` | integer | no |  | Google Trends category id (0 = all categories). |
| `gprop` | enum(images, news, froogle, youtube) | no |  | Property filter; omit for web search. |
| `tz` | integer | no |  | Time-zone offset in minutes (-1439..1439). |
| `q` | string | yes |  | Search query |
| `geo` | string | no |  | Geographic region (e.g. 'US', 'GB') |
| `date` | string | no |  | Time range (e.g. 'today 12-m', 'now 7-d') |
| `hl` | string | no | `en` | Language code (default 'en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "data_type": {
      "type": "string",
      "description": "What Trends returns (default: TIMESERIES). RELATED_QUERIES/RELATED_TOPICS and the GEO_MAP breakdowns are unreachable without it.",
      "enum": [
        "TIMESERIES",
        "GEO_MAP",
        "GEO_MAP_0",
        "RELATED_TOPICS",
        "RELATED_QUERIES"
      ]
    },
    "region": {
      "type": "string",
      "description": "Geographic granularity for the GEO_MAP data types.",
      "enum": [
        "COUNTRY",
        "REGION",
        "DMA",
        "CITY"
      ]
    },
    "cat": {
      "type": "integer",
      "description": "Google Trends category id (0 = all categories)."
    },
    "gprop": {
      "type": "string",
      "description": "Property filter; omit for web search.",
      "enum": [
        "images",
        "news",
        "froogle",
        "youtube"
      ]
    },
    "tz": {
      "type": "integer",
      "description": "Time-zone offset in minutes (-1439..1439)."
    },
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "geo": {
      "type": "string",
      "description": "Geographic region (e.g. 'US', 'GB')"
    },
    "date": {
      "type": "string",
      "description": "Time range (e.g. 'today 12-m', 'now 7-d')"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
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

Top-level keys: `search_metadata`, `search_parameters`, `interest_over_time`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_trends_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.prettify_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.date` | string |  |
| `search_parameters.tz` | string |  |
| `search_parameters.data_type` | string |  |
| `interest_over_time` | object |  |
| `interest_over_time.timeline_data[]` | array<object> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d7f1fad3627ae908052",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/d7NZdn8gfoOdJjoWwT5WxQ/69c83d7f1fad3627ae908052.json",
    "created_at": "2026-03-28 20:43:43 UTC",
    "processed_at": "2026-03-28 20:43:43 UTC",
    "google_trends_url": "https://trends.google.com/trends/embed/explore/TIMESERIES?hl=en&tz=420&req=%7B%22comparisonItem%22%3A%5B%7B%22keyword%22%3A%22instagram.com%22%2C%22geo%22%3A%22%22%2C%22time%22%3A%22today+
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

- `google_trends`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
