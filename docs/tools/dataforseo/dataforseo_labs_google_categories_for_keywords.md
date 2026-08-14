---
name: dataforseo_labs_google_categories_for_keywords
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_labs_google_categories_for_keywords`

Map a list of Google keywords (up to 1000) to IAB product/service categories.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `google`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_labs_google_categories_for_keywords",
  "params": {
    "keywords": []
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `keywords` | any[] | yes |  | Target keywords (up to 1000). UTF-8; converted to lowercase. |
| `language_name` | string | no |  | Full language name (e.g. 'English'). Required if language_code omitted. |
| `language_code` | string | no |  | ISO language code (e.g. 'en'). Required if language_name omitted. |
| `tag` | string | no |  | User-defined task identifier (≤255 chars). |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "keywords": {
      "type": "array",
      "description": "Target keywords (up to 1000). UTF-8; converted to lowercase."
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English'). Required if language_code omitted."
    },
    "language_code": {
      "type": "string",
      "description": "ISO language code (e.g. 'en'). Required if language_name omitted."
    },
    "tag": {
      "type": "string",
      "description": "User-defined task identifier (\u2264255 chars)."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `dataforseo_labs/google/categories_for_keywords/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "keywords"
  ]
}
```

## Example request

```json
{
  "keywords": []
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].language_code` | string |  |
| `[].items_count` | integer |  |
| `[].items[]` | array<object> |  |
| `[].items[].keyword` | string |  |
| `[].items[].categories[]` | array<integer> |  |

### Example response (from profile)

```json
[
  {
    "language_code": "en",
    "items_count": 2,
    "items": [
      {
        "keyword": "instagram",
        "categories": [
          10584,
          10108,
          13692,
          13691
        ]
      },
      {
        "keyword": "social media",
        "categories": [
          11494,
          13418,
          10007,
          11496
        ]
      }
    ]
  }
]
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

- `dataforseo_labs_google_keywords_for_categories`
- `dataforseo_kw_google_ads_keywords_for_keywords`
- `dataforseo_kw_google_ads_keywords_for_site`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
