---
name: serpapi_google_patents_details
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_google_patents_details`

Google Patents details for a specific patent via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `patents`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_google_patents_details",
  "params": {
    "patent_id": "patent_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `patent_id` | string | yes |  | Patent ID from Google Patents results |
| `hl` | string | no | `en` | Language code (default 'en') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "patent_id": {
      "type": "string",
      "description": "Patent ID from Google Patents results"
    },
    "hl": {
      "type": "string",
      "description": "Language code (default 'en')",
      "default": "en"
    }
  },
  "required": [
    "patent_id"
  ]
}
```

## Example request

```json
{
  "patent_id": "patent_id_example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `title`, `type`, `pdf`, `publication_number`, `country`, `prior_art_keywords`, `prior_art_date`, `application_number`, `inventors`, `assignees`, `priority_date`, `filing_date`, `publication_date`, `worldwide_applications`, `events`, `external_links`, `images`, `classifications`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.google_patents_details_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.patent_id` | string |  |
| `title` | string |  |
| `type` | string |  |
| `pdf` | string |  |
| `publication_number` | string |  |
| `country` | string |  |
| `prior_art_keywords[]` | array<string> |  |
| `prior_art_date` | string |  |
| `application_number` | string |  |
| `inventors[]` | array<object> |  |
| `inventors[].name` | string |  |
| `inventors[].link` | string |  |
| `inventors[].serpapi_link` | string |  |
| `assignees[]` | array<string> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c84ea3d45a3877c8478c40",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/T1Cn9ZF3HeHr6pVCoAtsWw/69c84ea3d45a3877c8478c40.json",
    "created_at": "2026-03-28 21:56:51 UTC",
    "processed_at": "2026-03-28 21:56:51 UTC",
    "google_patents_details_url": "https://patents.google.com/patent/US10769590B2/en",
    "raw_html_file": "https://serpapi.com/searches/T1Cn9ZF3HeHr6pVCoAtsWw/69c84ea3d45a3877c8478c40.html",
    "total_time_taken
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

**Chain inputs:** `{'param': 'patent_id', 'from_tool': 'serpapi_google_patents', 'extract': 'organic_results[].patent_id'}`

**Chain groups:** `serpapi_patents`

## Alternatives

- `google_patents_details`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
