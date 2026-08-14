---
name: spyfu_find_related_keywords
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_find_related_keywords`

Find semantically related keywords for a given query.

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
  "tool_name": "spyfu_find_related_keywords",
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
| `query` | string | yes |  | Keyword to find related keywords for |
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
      "description": "Keyword to find related keywords for"
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
| `results[].liveSearchVolume` | integer |  |
| `results[].rankingDifficulty` | integer |  |
| `results[].totalMonthlyClicks` | integer |  |
| `results[].percentMobileSearches` | number |  |
| `results[].percentDesktopSearches` | number |  |
| `results[].percentSearchesNotClicked` | number |  |
| `results[].percentPaidClicks` | number |  |
| `results[].percentOrganicClicks` | number |  |
| `results[].broadCostPerClick` | number |  |
| `results[].phraseCostPerClick` | number |  |
| `results[].exactCostPerClick` | number |  |
| `results[].broadMonthlyClicks` | integer |  |
| `results[].phraseMonthlyClicks` | number |  |
| `results[].exactMonthlyClicks` | integer |  |
| `results[].broadMonthlyCost` | number |  |
| `results[].phraseMonthlyCost` | number |  |
| `results[].exactMonthlyCost` | number |  |
| `results[].paidCompetitors` | integer |  |

### Example response (from profile)

```json
{
  "resultCount": 30,
  "totalMatchingResults": 260,
  "results": [
    {
      "keyword": "instagram.com",
      "searchVolume": 47300,
      "liveSearchVolume": 71600,
      "rankingDifficulty": 7,
      "totalMonthlyClicks": 41700,
      "percentMobileSearches": 0.547828761484991,
      "percentDesktopSearches": 0.452171238515009,
      "percentSearchesNotClicked": 0.118122160524987,
      "percentPaidClicks": 0.00586720091501614,
      "percentOrganicClicks": 0.994132798941881,
      "broad
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

- Keyword expansion: finds semantically related terms for SEO or PPC keyword lists
- Also available via spyfu_keyword_expansions with keyword_search_type='PhraseMatch'

## Alternatives

- `moz_keyword_difficulty`
- `moz_keyword_metrics`
- `moz_keyword_opportunity`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
