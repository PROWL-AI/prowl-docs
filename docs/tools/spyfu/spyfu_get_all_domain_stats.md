---
name: spyfu_get_all_domain_stats
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_all_domain_stats`

Get comprehensive domain statistics for ALL available historical periods.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `domain`, `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_get_all_domain_stats",
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

Top-level keys: `resultCount`, `domain`, `results`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `domain` | string |  |
| `results[]` | array<object> |  |
| `results[].searchMonth` | integer |  |
| `results[].searchYear` | integer |  |
| `results[].averageOrganicRank` | number |  |
| `results[].monthlyPaidClicks` | integer |  |
| `results[].averageAdRank` | integer |  |
| `results[].totalOrganicResults` | integer |  |
| `results[].monthlyBudget` | integer |  |
| `results[].monthlyOrganicValue` | number |  |
| `results[].totalAdsPurchased` | integer |  |
| `results[].monthlyOrganicClicks` | number |  |
| `results[].strength` | integer |  |
| `results[].totalInverseRank` | integer |  |

### Example response (from profile)

```json
{
  "resultCount": 1,
  "domain": "instagram.com",
  "results": [
    {
      "searchMonth": 2,
      "searchYear": 2011,
      "averageOrganicRank": 18.7,
      "monthlyPaidClicks": 0,
      "averageAdRank": 0,
      "totalOrganicResults": 34,
      "monthlyBudget": 0,
      "monthlyOrganicValue": 0.2803010154738878,
      "totalAdsPurchased": 0,
      "monthlyOrganicClicks": 1.3133429153463105,
      "strength": 5,
      "totalInverseRank": 0
    },
    {
      "searchMonth": 3,
      "searchY
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

- Full historical data — use for long-term trend analysis
- For recent trends only, spyfu_get_domain_stats (last N months) is faster

## Alternatives

- `moz_linking_domains`
- `moz_v2_global_top_root_domains`
- `moz_v2_linking_root_domains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
