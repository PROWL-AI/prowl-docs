---
name: serpapi_google
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google`

Google Web Search via SerpAPI — full results with knowledge graph, local pack.

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
  "tool_name": "serpapi_google",
  "params": {
    "q": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `device` | enum(desktop, tablet, mobile) | no |  | Device type. |
| `tbs` | string | no |  | Advanced search / date-range filter, e.g. 'qdr:m' for the past month. |
| `safe` | enum(active, off) | no |  | SafeSearch level. |
| `nfpr` | integer | no |  | 1 excludes auto-corrected results, 0 includes them. |
| `filter` | integer | no |  | 1 enables Google's similar/omitted-results filters, 0 disables them. |
| `lr` | string | no |  | Restrict results by language, e.g. 'lang_de' (pipe-separated for several). |
| `cr` | string | no |  | Restrict results by country of origin, e.g. 'countryDE'. |
| `google_domain` | string | no |  | Google domain to query, e.g. 'google.de'. |
| `uule` | string | no |  | Google-encoded location. Cannot be combined with `location`. |
| `q` | string | yes |  | Search query |
| `location` | string | no |  | Location for geo-targeted results (e.g. 'Austin, Texas') |
| `hl` | string | no | `en` | Language code (default 'en') |
| `gl` | string | no |  | Country code (e.g. 'us', 'gb') |
| `num` | integer | no |  | Number of results to return |
| `start` | integer | no |  | Result offset for pagination |
| `no_cache` | boolean | no |  | Force fresh crawl (no cached results) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "device": {
      "type": "string",
      "description": "Device type.",
      "enum": [
        "desktop",
        "tablet",
        "mobile"
      ]
    },
    "tbs": {
      "type": "string",
      "description": "Advanced search / date-range filter, e.g. 'qdr:m' for the past month."
    },
    "safe": {
      "type": "string",
      "description": "SafeSearch level.",
      "enum": [
        "active",
        "off"
      ]
    },
    "nfpr": {
      "type": "integer",
      "description": "1 excludes auto-corrected results, 0 includes them."
    },
    "filter": {
      "type": "integer",
      "description": "1 enables Google's similar/omitted-results filters, 0 disables them."
    },
    "lr": {
      "type": "string",
      "description": "Restrict results by language, e.g. 'lang_de' (pipe-separated for several)."
    },
    "cr": {
      "type": "string",
      "description": "Restrict results by country of origin, e.g. 'countryDE'."
    },
    "google_domain": {
      "type": "string",
      "description": "Google domain to query, e.g. 'google.de'."
    },
    "uule": {
      "type": "string",
      "description": "Google-encoded location. Cannot be combined with `location`."
    },
    "q": {
      "type": "string",
      "description": "Search query"
    },
    "location": {
      "type": "string",
      "description": "Location for geo-targeted results (e.g. 'Austin, Texas')"
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
    "num": {
      "type": "integer",
      "description": "Number of results to return",
      "minimum": 1,
      "maximum": 100
    },
    "start": {
      "type": "integer",
      "description": "Result offset for pagination"
    },
    "no_cache": {
      "type": "boolean",
      "description": "Force fresh crawl (no cached results)"
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

Top-level keys: `search_metadata`, `search_parameters`, `search_information`, `related_questions`, `organic_results`, `latest_posts`, `pagination`, `serpapi_pagination`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.pixel_position_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.q` | string |  |
| `search_parameters.google_domain` | string |  |
| `search_parameters.hl` | string |  |
| `search_parameters.device` | string |  |
| `search_information` | object |  |
| `search_information.query_displayed` | string |  |
| `search_information.total_results` | integer |  |
| `search_information.time_taken_displayed` | number |  |
| `search_information.organic_results_state` | string |  |
| `related_questions[]` | array<object> |  |
| `related_questions[].question` | string |  |
| `related_questions[].type` | string |  |
| `related_questions[].link` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c83d77f9c5e93dbdc9ac39",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/XxkuJTmrQZ6KI0XDFpJvrw/69c83d77f9c5e93dbdc9ac39.json",
    "pixel_position_endpoint": "https://serpapi.com/searches/XxkuJTmrQZ6KI0XDFpJvrw/69c83d77f9c5e93dbdc9ac39.json_with_pixel_position",
    "created_at": "2026-03-28 20:43:35 UTC",
    "processed_at": "2026-03-28 20:43:35 UTC",
    "google_url": "https://www.google.com/search?q=instagram.com&oq=instagram.
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

- `google_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
