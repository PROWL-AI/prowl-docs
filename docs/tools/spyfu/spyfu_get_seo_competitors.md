---
name: spyfu_get_seo_competitors
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_seo_competitors`

Get top SEO-only competitors — domains competing in organic search only.

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
  "tool_name": "spyfu_get_seo_competitors",
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

Top-level keys: `resultCount`, `totalMatchingResults`, `results`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer |  |
| `totalMatchingResults` | integer |  |
| `results[]` | array<object> |  |
| `results[].domain` | string |  |
| `results[].commonTerms` | integer |  |
| `results[].rank` | number |  |

### Example response (from profile)

```json
{
  "resultCount": 5,
  "totalMatchingResults": 501,
  "results": [
    {
      "domain": "facebook.com",
      "commonTerms": 69072089,
      "rank": 0.5959615
    },
    {
      "domain": "youtube.com",
      "commonTerms": 64796120,
      "rank": 0.46715394
    },
    {
      "domain": "reddit.com",
      "commonTerms": 56928070,
      "rank": 0.328708
    },
    {
      "domain": "tiktok.com",
      "commonTerms": 43445350,
      "rank": 0.18861188
    },
    {
      "domain": "wikipedia.org
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

- SEO analysis workflow: focused organic competitor list
- For combined organic+paid competitors, use spyfu_get_combined_competitors instead
- Pair with spyfu_get_ppc_competitors for organic vs paid competitor comparison

## Alternatives

- `spyfu_get_combined_competitors`
- `spyfu_get_ppc_competitors`
- `dataforseo_labs_competitors_domain`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
