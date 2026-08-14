---
name: spyfu_get_new_top_pages
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_new_top_pages`

Get newly discovered top pages for a domain — pages that recently started ranking well.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `onpage`, `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_get_new_top_pages",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | Domain name (e.g. 'example.com') |
| `page_size` | integer | no | `30` | Number of results (default: 30) |
| `country_code` | enum(AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA) | no | `US` | Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Domain name (e.g. 'example.com')"
    },
    "page_size": {
      "type": "integer",
      "description": "Number of results (default: 30)",
      "default": 30,
      "minimum": 1
    },
    "country_code": {
      "type": "string",
      "description": "Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US",
      "enum": [
        "AR",
        "AT",
        "AU",
        "BE",
        "BR",
        "CA",
        "CH",
        "DE",
        "DK",
        "ES",
        "FR",
        "IE",
        "IN",
        "IT",
        "JP",
        "MX",
        "NL",
        "NO",
        "NZ",
        "PL",
        "PT",
        "SE",
        "SG",
        "TR",
        "UA",
        "UK",
        "US",
        "ZA"
      ],
      "default": "US"
    }
  },
  "required": [
    "domain"
  ]
}
```

## Example request

```json
{
  "domain": "example.com"
}
```

## Output

Top-level keys: `resultCount`, `results`, `totalMatchingResults`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `results[]` | array<object> |  |
| `results[].title` | string |  |
| `results[].url` | string |  |
| `results[].keywordCount` | integer |  |
| `results[].estMonthlySeoClicks` | integer |  |
| `results[].topKeyword` | string |  |
| `results[].topKeywordPosition` | integer |  |
| `results[].topKeywordSearchVolume` | null |  |
| `results[].topKeywordClicks` | integer |  |
| `totalMatchingResults` | integer |  |

### Example response (from profile)

```json
{
  "resultCount": 30,
  "results": [
    {
      "title": "This is amazing 💀 A new tool developed by the search engine Kagi functions as a direct translator for LinkedIn language. The feature allows users to input everyday sentences and instantly converts them into the specific corporate phrasing commonly found on the networking platform. Operating similarly to Google Translate, the application analyzes the original text and rewrites it using professional terminology and networking-oriented for
...
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid SPYFY_APP_ID or SPYFY_API_SECRET | Skip SpyFu tools — report that SEO data is unavailable |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 404 | Domain not found in SpyFu database | Domain may be too new/small; try with a larger competitor domain |

## When to use

- Competitive gap analysis: detect new content strategies or landing pages
- Combine with spyfu_get_new_ppc_keywords to see both content and PPC changes

## Alternatives

- `moz_top_pages`
- `moz_v2_global_top_pages`
- `moz_v2_top_pages`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
