---
name: dataforseo_serp_yahoo_organic
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_serp_yahoo_organic`

Fetch Yahoo web search results (organic) in real time.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_serp_yahoo_organic",
  "params": {
    "keyword": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keyword` | string | yes |  | Search query (up to 700 chars). UTF-8 encoded. |
| `location_name` | string | no |  | Full location name (e.g. 'United States'). One of location_name or location_code required. |
| `location_code` | integer | no |  | Location code (e.g. 2840 for US). One of location_name or location_code required. |
| `language_name` | string | no |  | Full language name (e.g. 'English'). One of language_name or language_code required. |
| `language_code` | string | no |  | Language code (e.g. 'en'). One of language_name or language_code required. |
| `device` | enum(desktop, mobile) | no |  | Device type: 'desktop' or 'mobile'. Default: desktop. |
| `os` | string | no |  | Operating system for device context (windows/macos or android/ios). |
| `depth` | integer | no |  | Number of results to return. Default and max vary by engine. |
| `max_crawl_pages` | integer | no |  | Number of SERP pages to crawl (max 100). Complements depth. |
| `url` | string | no |  | Direct Yahoo search URL to parse (alternative to keyword+location). |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keyword": {
      "type": "string",
      "description": "Search query (up to 700 chars). UTF-8 encoded."
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States'). One of location_name or location_code required."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840 for US). One of location_name or location_code required."
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English'). One of language_name or language_code required."
    },
    "language_code": {
      "type": "string",
      "description": "Language code (e.g. 'en'). One of language_name or language_code required."
    },
    "device": {
      "type": "string",
      "description": "Device type: 'desktop' or 'mobile'. Default: desktop.",
      "enum": [
        "desktop",
        "mobile"
      ]
    },
    "os": {
      "type": "string",
      "description": "Operating system for device context (windows/macos or android/ios)."
    },
    "depth": {
      "type": "integer",
      "description": "Number of results to return. Default and max vary by engine."
    },
    "max_crawl_pages": {
      "type": "integer",
      "description": "Number of SERP pages to crawl (max 100). Complements depth."
    },
    "url": {
      "type": "string",
      "description": "Direct Yahoo search URL to parse (alternative to keyword+location)."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `serp/yahoo/organic/live/advanced` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "keyword"
  ]
}
```

## Example request

```json
{
  "keyword": "example query"
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].keyword` | string |  |
| `[].type` | string |  |
| `[].se_domain` | string |  |
| `[].location_code` | integer |  |
| `[].language_code` | string |  |
| `[].check_url` | string |  |
| `[].datetime` | string |  |
| `[].spell` | null |  |
| `[].refinement_chips` | null |  |
| `[].item_types` | null |  |
| `[].se_results_count` | integer |  |
| `[].pages_count` | integer |  |
| `[].items_count` | integer |  |
| `[].items` | null |  |

### Example response (from profile)

```json
[
  {
    "keyword": "instagram",
    "type": "organic",
    "se_domain": "us.search.yahoo.com",
    "location_code": 2840,
    "language_code": "en",
    "check_url": "https://us.search.yahoo.com/search?p=instagram&vl=lang_en&ei=UTF-8&fl=1&lat=37.09024&lon=-95.712891&locupdate=1&radius=150&fr2=p%3As%2Cv%3Aw%2Cm%3Aloc",
    "datetime": "2026-08-11 18:41:13 +00:00",
    "spell": null,
    "refinement_chips": null,
    "item_types": null,
    "se_results_count": 0,
    "pages_count": 1,
    "items
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

## Alternatives

- `serpapi_yahoo`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
