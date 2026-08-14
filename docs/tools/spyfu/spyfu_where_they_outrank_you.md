---
name: spyfu_where_they_outrank_you
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_where_they_outrank_you`

Get keywords where a specific competitor outranks your domain organically.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SpyFu |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `seo`, `spyfu` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "spyfu_where_they_outrank_you",
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
| `domain` | string | yes |  | Your domain (e.g. 'example.com') |
| `competitor` | string | yes |  | Competitor domain (e.g. 'rival.com') |
| `page_size` | integer | no | `30` | Number of results (default: 30) |
| `country_code` | enum(AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA) | no | `US` | Two-letter country code. Supported: AR, AT, AU, BE, BR, CA, CH, DE, DK, ES, FR, IE, IN, IT, JP, MX, NL, NO, NZ, PL, PT, SE, SG, TR, UA, UK, US, ZA. Default: US |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "domain": {
      "type": "string",
      "description": "Your domain (e.g. 'example.com')"
    },
    "competitor": {
      "type": "string",
      "description": "Competitor domain (e.g. 'rival.com')"
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

Top-level keys: `type`, `title`, `status`, `traceId`, `errors`

| Path | Type | Description |
|------|------|-------------|
| `type` | string |  |
| `title` | string |  |
| `status` | integer |  |
| `traceId` | string |  |
| `errors` | object |  |
| `errors.CompareDomain[]` | array<string> |  |

### Example response (from profile)

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "One or more validation errors occurred.",
  "status": 400,
  "traceId": "00-41584cda811ce10657480400fb931c53-c5862d7ea21ae3d2-00",
  "errors": {
    "CompareDomain": [
      "The CompareDomain field is required."
    ]
  }
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

- Kombat tool — find keywords where competitor beats you (gap analysis)
- Combine with spyfu_organic_outranking_keywords for full head-to-head view
- Part of Kombat workflow: use with spyfu_competing_seo_keywords and spyfu_competing_ppc_keywords
- Also key for competitive gap analysis with spyfu_get_bulk_domain_stats

## Alternatives

_None listed._

## Provider docs

https://developer.spyfu.com/reference
