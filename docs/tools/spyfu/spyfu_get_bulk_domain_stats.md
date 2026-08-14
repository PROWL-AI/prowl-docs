---
name: spyfu_get_bulk_domain_stats
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_bulk_domain_stats`

Get snapshot stats for multiple domains in a single API call.

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
  "tool_name": "spyfu_get_bulk_domain_stats",
  "params": {
    "domains": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domains` | string[] | yes |  | List of domain names to get stats for (max 10) |
| `country_code` | enum(AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA) | no | `US` | Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domains": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "List of domain names to get stats for (max 10)",
      "maxItems": 10
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
    "domains"
  ]
}
```

## Example request

```json
{
  "domains": "example.com"
}
```

## Output

Top-level keys: `resultCount`, `results`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `results[]` | array<object> |  |
| `results[].domain` | string |  |
| `results[].results[]` | array<object> |  |

### Example response (from profile)

```json
{
  "resultCount": 1,
  "results": [
    {
      "domain": "instagram.com",
      "results": [
        {
          "searchMonth": 2,
          "searchYear": 2026,
          "averageOrganicRank": 52,
          "monthlyPaidClicks": 855500,
          "averageAdRank": 1.9,
          "totalOrganicResults": 512000000,
          "monthlyBudget": 2682000,
          "monthlyOrganicValue": 1016000000,
          "totalAdsPurchased": 4002,
          "monthlyOrganicClicks": 402000000,
          "strength": 8
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

- Competitive gap analysis: compare stats across multiple domains in one call
- Pass up to 10 domains — use after spyfu_get_combined_competitors or spyfu_find_matching_domains
- More efficient than calling spyfu_get_domain_stats for each domain separately

## Alternatives

- `spyfu_get_domain_stats`
- `dataforseo_labs_bulk_traffic_estimation`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
