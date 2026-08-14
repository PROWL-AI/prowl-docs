---
name: serpapi_facebook_profile
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_facebook_profile`

Facebook public profile data via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `facebook`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_facebook_profile",
  "params": {
    "profile_id": "profile_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `profile_id` | string | yes |  | Facebook profile ID (numeric) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "profile_id": {
      "type": "string",
      "description": "Facebook profile ID (numeric)"
    }
  },
  "required": [
    "profile_id"
  ]
}
```

## Example request

```json
{
  "profile_id": "profile_id_example"
}
```

## Output

Top-level keys: `search_metadata`, `search_parameters`, `profile_results`

| Path | Type | Description |
|------|------|-------------|
| `search_metadata` | object |  |
| `search_metadata.id` | string |  |
| `search_metadata.status` | string |  |
| `search_metadata.json_endpoint` | string |  |
| `search_metadata.created_at` | string |  |
| `search_metadata.processed_at` | string |  |
| `search_metadata.facebook_profile_url` | string |  |
| `search_metadata.raw_html_file` | string |  |
| `search_metadata.total_time_taken` | number |  |
| `search_parameters` | object |  |
| `search_parameters.engine` | string |  |
| `search_parameters.profile_id` | string |  |
| `profile_results` | object |  |
| `profile_results.name` | string |  |
| `profile_results.id` | string |  |
| `profile_results.url` | string |  |
| `profile_results.gender` | string |  |
| `profile_results.verified` | boolean |  |
| `profile_results.profile_picture` | string |  |
| `profile_results.cover_photo` | string |  |
| `profile_results.followers` | string |  |
| `profile_results.following` | string |  |
| `profile_results.profile_type` | string |  |
| `profile_results.profile_intro_text` | string |  |
| `profile_results.category` | string |  |

### Example response (from profile)

```json
{
  "search_metadata": {
    "id": "69c84ea8b7942f47c3eda315",
    "status": "Success",
    "json_endpoint": "https://serpapi.com/searches/oPuNbgHP_-nbyZPDWWczgg/69c84ea8b7942f47c3eda315.json",
    "created_at": "2026-03-28 21:56:56 UTC",
    "processed_at": "2026-03-28 21:56:56 UTC",
    "facebook_profile_url": "https://www.facebook.com/instagram",
    "raw_html_file": "https://serpapi.com/searches/oPuNbgHP_-nbyZPDWWczgg/69c84ea8b7942f47c3eda315.html",
    "total_time_taken": 2.59
  },
  "searc
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

**Chain groups:** `serpapi_places`

## Alternatives

- `serpapi_amazon`
- `serpapi_apple_app_store`
- `serpapi_baidu`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
