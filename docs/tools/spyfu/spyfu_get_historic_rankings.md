---
name: spyfu_get_historic_rankings
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_get_historic_rankings`

Get historical keyword ranking changes for a domain over a time period.

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
  "tool_name": "spyfu_get_historic_rankings",
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
| `query_type` | enum(MostValuable, FellFromTop10, MadeTheTop10, NewKeywords, NoLongerRanks, GainedRanks, LostRanks, GainedClicks, LostClicks) | no | `MostValuable` | Type of ranking data |
| `start_date` | string | no |  | Start date (YYYY-MM-DD format, optional) |
| `end_date` | string | no |  | End date (YYYY-MM-DD format, optional) |
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
    "query_type": {
      "type": "string",
      "description": "Type of ranking data",
      "enum": [
        "MostValuable",
        "FellFromTop10",
        "MadeTheTop10",
        "NewKeywords",
        "NoLongerRanks",
        "GainedRanks",
        "LostRanks",
        "GainedClicks",
        "LostClicks"
      ],
      "default": "MostValuable"
    },
    "start_date": {
      "type": "string",
      "description": "Start date (YYYY-MM-DD format, optional)"
    },
    "end_date": {
      "type": "string",
      "description": "End date (YYYY-MM-DD format, optional)"
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

Top-level keys: `type`, `title`, `status`, `traceId`, `errors`

| Path | Type | Description |
|------|------|-------------|
| `type` | string |  |
| `title` | string |  |
| `status` | integer |  |
| `traceId` | string |  |
| `errors` | object |  |
| `errors.StartDate[]` | array<string> |  |

### Example response (from profile)

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
  "title": "One or more validation errors occurred.",
  "status": 400,
  "traceId": "00-9d761610704b84d51e0a3fd694e38af3-0cfed7e4e791db4a-00",
  "errors": {
    "StartDate": [
      "Cannot return history before October 2020"
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

- Track ranking changes over time — use query_type to focus on gains, losses, or new keywords
- Combine with spyfu_get_domain_stats for traffic-level trends

## Alternatives

_None listed._

## Provider docs

https://developer.spyfu.com/reference
