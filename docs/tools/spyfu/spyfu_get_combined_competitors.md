---
name: spyfu_get_combined_competitors
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_combined_competitors`

Get the combined top competitors for a domain based on both organic and paid search overlap.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `competitors`, `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_get_combined_competitors",
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

Top-level keys: `resultCount`, `totalMatchingResults`, `combinedCompetitors`, `ppcCompetitors`, `seoCompetitors`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `totalMatchingResults` | integer |  |
| `combinedCompetitors[]` | array<object> |  |
| `combinedCompetitors[].rank` | number |  |
| `combinedCompetitors[].domain` | string |  |
| `ppcCompetitors[]` | array<object> |  |
| `ppcCompetitors[].domain` | string |  |
| `ppcCompetitors[].commonTerms` | integer |  |
| `ppcCompetitors[].rank` | number |  |
| `seoCompetitors[]` | array<object> |  |
| `seoCompetitors[].domain` | string |  |
| `seoCompetitors[].commonTerms` | integer |  |
| `seoCompetitors[].rank` | number |  |

### Example response (from profile)

```json
{
  "resultCount": 5,
  "totalMatchingResults": 550,
  "combinedCompetitors": [
    {
      "rank": 0.5959615,
      "domain": "facebook.com"
    },
    {
      "rank": 0.46715394,
      "domain": "youtube.com"
    },
    {
      "rank": 0.328708,
      "domain": "reddit.com"
    },
    {
      "rank": 0.18861188,
      "domain": "tiktok.com"
    },
    {
      "rank": 0.16958438,
      "domain": "wikipedia.org"
    }
  ],
  "ppcCompetitors": [
    {
      "domain": "blueribbonwindowcleaning.com
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

- Find competitors workflow: use for SEO/PPC competitor discovery
- Combine with exa_similar_search for URL-based discovery
- Follow up with spyfu_get_bulk_domain_stats to compare discovered competitors
- Feed results into gemini_extract_competitors for structured output

## Alternatives

- `dataforseo_labs_competitors_domain`
- `exa_similar_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
