---
name: spyfu_get_paid_search
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_paid_search`

Get active paid search ads and keywords for a domain.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `search`, `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_get_paid_search",
  "params": {
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `adult_filter` | boolean | no |  | Exclude adult keywords considered unsafe. SpyFu's own default is true; set false to include them. |
| `starting_row` | integer | no |  | Row number to start results with (1-10000) — the only way to read past the first page. |
| `domain` | string | yes |  | Domain name (e.g. 'example.com') |
| `page_size` | integer | no | `100` | Number of results (default: 100) |
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
    "domain": {
      "type": "string",
      "description": "Domain name (e.g. 'example.com')"
    },
    "page_size": {
      "type": "integer",
      "description": "Number of results (default: 100)",
      "default": 100,
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
| `results[].keyword` | string |  |
| `results[].termId` | string |  |
| `results[].adPosition` | integer |  |
| `results[].adCount` | integer |  |
| `results[].dateSearched` | string |  |
| `results[].title` | string |  |
| `results[].bodyHtml` | string |  |
| `results[].domain` | string |  |
| `results[].searchVolume` | integer |  |
| `results[].keywordDifficulty` | integer |  |
| `results[].isNsfw` | null |  |
| `totalMatchingResults` | integer |  |

### Example response (from profile)

```json
{
  "resultCount": 100,
  "results": [
    {
      "keyword": "instagram",
      "termId": "28150305",
      "adPosition": 1,
      "adCount": 1,
      "dateSearched": "2024-06-16T00:00:00Z",
      "title": "Create, Share, Connect | Get Creative with Stories",
      "bodyHtml": "<div class=\"v5yQqb\"><a class=\"sVXRqc\" data-agch=\"HJ3bqe\" data-impdclcc=\"1\" data-agdh=\"fvd3vc\" data-rw=\"https://www.google.it/aclk?sa=L&amp;ai=DChcSEwjhwpyphN-GAxV4noMHHa-XDrQYABAAGgJlZg&amp;gclid=EAIaIQobChMI4
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

- See what Google Search ads a domain is currently running
- For historical ad copy evolution, use spyfu_get_ad_history instead
- For keyword-level ad research, use spyfu_get_term_ad_history_with_stats

## Alternatives

- `moz_search_intent`
- `majestic_search_by_keyword`
- `firecrawl_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
