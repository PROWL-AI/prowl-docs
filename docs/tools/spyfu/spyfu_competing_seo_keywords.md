---
name: spyfu_competing_seo_keywords
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_competing_seo_keywords`

Head-to-head SEO keyword comparison between two domains (Kombat API).

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
  "tool_name": "spyfu_competing_seo_keywords",
  "params": {
    "competitor": "competitor.com",
    "domain": "example.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `domain` | string | yes |  | First domain (e.g. 'example.com') |
| `competitor` | string | yes |  | Second domain to compare against |
| `page_size` | integer | no | `30` | Number of results (default: 30) |
| `country_code` | enum(AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA) | no | `US` | Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "First domain (e.g. 'example.com')"
    },
    "competitor": {
      "type": "string",
      "description": "Second domain to compare against"
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
    "domain",
    "competitor"
  ]
}
```

## Example request

```json
{
  "competitor": "competitor.com",
  "domain": "example.com"
}
```

## Output

Top-level keys: `type`, `title`, `status`, `errors`, `traceId`

| Path | Type | Description |
|------|------|-------------|
| `type` | string |  |
| `title` | string |  |
| `status` | integer |  |
| `errors` | object |  |
| `errors.IncludeDomainsCsv[]` | array<string> |  |
| `traceId` | string |  |

### Example response (from profile)

```json
{
  "type": "https://tools.ietf.org/html/rfc9110#section-15.5.1",
  "title": "One or more validation errors occurred.",
  "status": 400,
  "errors": {
    "IncludeDomainsCsv": [
      "The IncludeDomainsCsv field is required.",
      "IncludeDomainsCsv cannot be empty"
    ]
  },
  "traceId": "00-a075ad18402c6d9aae85dda67129f308-f07e86c9813eb807-00"
}
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid SPYFY_APP_ID or SPYFY_API_SECRET | Skip SpyFu tools — report that SEO data is unavailable |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 404 | Domain not found in SpyFu database | Domain may be too new/small; try with a larger competitor domain |

## When to use

- Kombat tool — head-to-head SEO keyword comparison between two domains
- Combine with spyfu_competing_ppc_keywords for full keyword overlap analysis
- Essential for competitive SEO strategy and content gap analysis

## Alternatives

- `dataforseo_labs_domain_intersection`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
