---
name: spyfu_organic_outranking_keywords
provider: SpyFu
provider_slug: spyfu
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `spyfu_organic_outranking_keywords`

Get keywords where your domain outranks a specific competitor organically.

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
  "tool_name": "spyfu_organic_outranking_keywords",
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

Keywords where the query domain outranks compareDomain organically (Kombat SEO outranking list)

Top-level keys: `resultCount`, `results`, `totalMatchingResults`

| Path | Type | Description |
|------|------|-------------|
| `resultCount` | integer | Number of keyword rows returned on this page |
| `results[]` | array<object> | Outranking keyword rows |
| `results[].keyword` | string | Keyword phrase |
| `results[].rank` | integer | Organic rank of the query domain |
| `results[].compareRank` | integer | Organic rank of the competitor (compareDomain) |
| `results[].searchVolume` | integer | Monthly search volume |
| `results[].keywordDifficulty` | integer | SpyFu keyword difficulty score |
| `results[].topRankedUrl` | string | Top-ranked URL for the keyword when present |
| `totalMatchingResults` | integer | Total matching keywords across pages |

### Example response (from profile)

```json
{"resultCount": 2, "results": [{"keyword": "example crm", "rank": 3, "compareRank": 12, "searchVolume": 2400, "keywordDifficulty": 45, "topRankedUrl": "https://example.com/crm"}], "totalMatchingResults": 2}
```

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid SPYFY_APP_ID or SPYFY_API_SECRET | Skip SpyFu tools — report that SEO data is unavailable |
| 429 | Rate limit exceeded | Wait 30s and retry once |
| 404 | Domain not found in SpyFu database | Domain may be too new/small; try with a larger competitor domain |

## When to use

- Kombat tool — find keywords where you beat the competitor (your strengths)
- Inverse of spyfu_where_they_outrank_you — use both for full head-to-head view
- Part of Kombat workflow: combine with spyfu_competing_seo_keywords and spyfu_competing_ppc_keywords

## Alternatives

- `moz_keyword_difficulty`
- `moz_keyword_metrics`
- `moz_keyword_opportunity`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer.spyfu.com/reference
