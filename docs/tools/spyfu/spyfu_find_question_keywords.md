---
name: spyfu_find_question_keywords
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_find_question_keywords`

Find question-form keywords related to a query (e.g.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `keywords`, `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_find_question_keywords",
  "params": {
    "query": "example query"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `adult_filter` | boolean | no |  | Exclude adult keywords considered unsafe. SpyFu's own default is true; set false to include them. |
| `starting_row` | integer | no |  | Row number to start results with (1-10000) — the only way to read past the first page. |
| `query` | string | yes |  | Keyword to find question variants for |
| `page_size` | integer | no | `30` | Number of results (default: 30) |
| `country_code` | enum(AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA) | no | `US` | Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "adult_filter": {
      "type": "boolean",
      "description": "Exclude adult keywords considered unsafe. SpyFu's own default is true; set false to include them."
    },
    "starting_row": {
      "type": "integer",
      "description": "Row number to start results with (1-10000) \u2014 the only way to read past the first page.",
      "minimum": 1,
      "maximum": 10000
    },
    "query": {
      "type": "string",
      "description": "Keyword to find question variants for"
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
    "query"
  ]
}
```

## Example request

```json
{
  "query": "example query"
}
```

## Output

Top-level keys: `resultCount`, `totalMatchingResults`, `results`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `totalMatchingResults` | integer |  |
| `results[]` | array<object> |  |
| `results[].keyword` | string |  |
| `results[].searchVolume` | integer |  |
| `results[].liveSearchVolume` | null |  |
| `results[].rankingDifficulty` | null |  |
| `results[].totalMonthlyClicks` | integer |  |
| `results[].percentMobileSearches` | null |  |
| `results[].percentDesktopSearches` | null |  |
| `results[].percentSearchesNotClicked` | null |  |
| `results[].percentPaidClicks` | null |  |
| `results[].percentOrganicClicks` | null |  |
| `results[].broadCostPerClick` | null |  |
| `results[].phraseCostPerClick` | null |  |
| `results[].exactCostPerClick` | null |  |
| `results[].broadMonthlyClicks` | null |  |
| `results[].phraseMonthlyClicks` | null |  |
| `results[].exactMonthlyClicks` | null |  |
| `results[].broadMonthlyCost` | null |  |
| `results[].phraseMonthlyCost` | null |  |
| `results[].exactMonthlyCost` | null |  |
| `results[].paidCompetitors` | null |  |

### Example response (from profile)

```json
{
  "resultCount": 3,
  "totalMatchingResults": 3,
  "results": [
    {
      "keyword": "instagram.com down?",
      "searchVolume": 250,
      "liveSearchVolume": null,
      "rankingDifficulty": null,
      "totalMonthlyClicks": 250,
      "percentMobileSearches": null,
      "percentDesktopSearches": null,
      "percentSearchesNotClicked": null,
      "percentPaidClicks": null,
      "percentOrganicClicks": null,
      "broadCostPerClick": null,
      "phraseCostPerClick": null,
      "exac
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

- Content marketing: find question-form keywords for FAQ pages and blog content
- Also available via spyfu_keyword_expansions with keyword_search_type='Questions'

## Alternatives

- `moz_keyword_difficulty`
- `moz_keyword_metrics`
- `moz_keyword_opportunity`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
