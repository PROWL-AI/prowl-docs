---
name: majestic_get_ref_domains
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_ref_domains`

Referring domains for 1-4 items with TrustFlow/CitationFlow, geo, TLD, matched-link counts; with 2+ items returns cross-match intersection (domains linking to several competitor...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `domain`, `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_ref_domains",
  "params": {
    "items": [
      "majestic.com",
      "ahrefs.com"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `items` | string[] | yes |  | 1-4 domains/subdomains/URLs (2+ enables cross-matching) |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `count` | integer | no | `100` |  |
| `analysis_depth` | integer | no | `10000` | Referring domains analyzed per root |
| `min_matches_required` | integer | no | `1` |  |
| `order_by` | integer | no |  | Sort field index: 0=matches 1=AlexaRank 2=refRootDomains 3=extBackLinks 11=matchedLinks 12=CitationFlow 13=TrustFlow |
| `order_dir` | enum(0, 1) | no |  | 1=desc, 0=asc |
| `use_prefix_scan` | boolean | no | `False` |  |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "items": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "maxItems": 4,
      "description": "1-4 domains/subdomains/URLs (2+ enables cross-matching)"
    },
    "datasource": {
      "type": "string",
      "enum": [
        "fresh",
        "historic"
      ],
      "default": "fresh",
      "description": "Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data)"
    },
    "count": {
      "type": "integer",
      "default": 100,
      "minimum": 1
    },
    "analysis_depth": {
      "type": "integer",
      "default": 10000,
      "minimum": 1,
      "maximum": 100000,
      "description": "Referring domains analyzed per root"
    },
    "min_matches_required": {
      "type": "integer",
      "default": 1,
      "minimum": 1,
      "maximum": 4
    },
    "order_by": {
      "type": "integer",
      "minimum": 0,
      "maximum": 18,
      "description": "Sort field index: 0=matches 1=AlexaRank 2=refRootDomains 3=extBackLinks 11=matchedLinks 12=CitationFlow 13=TrustFlow"
    },
    "order_dir": {
      "type": "integer",
      "enum": [
        0,
        1
      ],
      "description": "1=desc, 0=asc"
    },
    "use_prefix_scan": {
      "type": "boolean",
      "default": false
    }
  },
  "required": [
    "items"
  ]
}
```

## Example request

```json
{
  "items": [
    "majestic.com",
    "ahrefs.com"
  ]
}
```

## Output

DataTables.Results rows (one per referring domain)

Key fields: `DataTables.Results.Data[].Domain`, `DataTables.Results.Data[].TrustFlow`, `DataTables.Results.Data[].Matches`, `DataTables.Results.Data[].MatchedLinks`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| invalid_api_key | Majestic rejected the API key (Code != OK, e.g. InvalidAPIKey). | Verify MAJESTIC_API_KEY and that API access is enabled on the Majestic account (API tab). |
| insufficient_units | Analysis / retrieval / index-item resource units exhausted for the billing period. | Check remaining units via majestic_get_subscription_info; reduce count/items or wait for period reset. |
| rate_limit | Too many requests (SearchByKeyword is limited to 3 requests/second per account). | Retry with backoff; the provider pool already throttles concurrency. |
| invalid_item | Item/domain/URL malformed or not present in the chosen index. | Pass a bare root domain (example.com), subdomain, or full URL; try datasource=historic for older items. |
| prefix_scan_not_possible | use_prefix_scan=True failed with RealTimePrefixQueryNotPossible for a large item. | Pre-check with majestic_get_prefix_query_estimate; fall back to majestic_download_back_links. |

## When to use

- Pass your domain + 3 competitors and min_matches_required=2 for a link-gap shortlist
- >100k referring domains needs the majestic_download_ref_domain_back_links job

## Alternatives

- `dataforseo_bl_referring_domains`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
