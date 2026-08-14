---
name: google_patents_details
provider: SearchAPI.io
provider_slug: searchapi
category: searchapi
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `google_patents_details`

Google Patents Details — full patent details including claims, description, and citations.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SearchAPI.io |
| Category | `searchapi` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `google`, `patents`, `searchapi` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "google_patents_details",
  "params": {
    "patent_id": "patent_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `patent_id` | string | yes |  | Patent ID (e.g. 'US10000000B2') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "patent_id": {
      "type": "string",
      "description": "Patent ID (e.g. 'US10000000B2')"
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
| `search_metadata.created_at` | string |  |
| `search_metadata.request_time_taken` | number |  |
| `search_metadata.parsing_time_taken` | number |  |
| `search_metadata.total_time_taken` | number |  |
| `search_metadata.request_url` | string |  |
| `search_metadata.html_url` | string |  |
| `search_metadata.json_url` | string |  |
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
| `assignees[]` | array<string> |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "search_MG6OPWeEVjFx9wwWA4jR8w7N",
    "status": "Success",
    "created_at": "2026-03-28T21:56:29Z",
    "request_time_taken": 0.69,
    "parsing_time_taken": 0.03,
    "total_time_taken": 0.72,
    "request_url": "https://patents.google.com/patent/US10769590B2/en",
    "html_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9wwWA4jR8w7N.html",
    "json_url": "https://www.searchapi.io/api/v1/searches/search_MG6OPWeEVjFx9wwWA4jR8w7N"
  },
  "s
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

**Chain inputs:** `{'param': 'patent_id', 'from_tool': 'google_patents', 'extract': 'organic_results[].patent_id'}`

**Chain groups:** `searchapi_patents`

## Alternatives

- `serpapi_google_patents_details`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://www.searchapi.io/docs
