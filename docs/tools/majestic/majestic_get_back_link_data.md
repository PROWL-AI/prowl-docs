---
name: majestic_get_back_link_data
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_back_link_data`

Backlink rows for a domain/subdomain/URL from Majestic (up to 50,000): source URL/title, anchor text, link type + flags (nofollow/deleted/redirect), first/last seen dates, sourc...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_back_link_data",
  "params": {
    "item": "majestic.com"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `item` | string | yes |  | Domain, subdomain, or full URL |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `count` | integer | no | `100` |  |
| `from_offset` | integer | no | `0` | Paging offset |
| `mode` | enum(0, 1) | no | `0` | 0=include deleted links; 1=exclude deleted |
| `show_domain_info` | boolean | no | `False` | Add a referring-domain info table |
| `max_source_urls_per_ref_domain` | enum(-1, 1, 3, 10) | no | `-1` |  |
| `ref_domain` | string | no |  | Only top-10 backlinks from this referring domain |
| `filter_topic` | string | no |  | Topical Trust Flow topic filter, e.g. 'Computers/Programming' |
| `use_prefix_scan` | boolean | no | `False` | Treat item as path prefix (example.com/blog*) |
| `enable_sorting_filtering` | boolean | no | `False` | Enable sort_by/filters + stats tables (+5000 analysis units) |
| `sort_by` | enum(AnchorText, DateDeleted, DomainCitationFlow, DomainTrustFlow, ExternalOutlinks, FirstSeen, InternalOutlinks, LastSeen, OutDomainsExternal, SourceCitationFlow, SourceTrustFlow, SourceUrl, TargetUrlLength, TotalOutlinks) | no |  | Requires enable_sorting_filtering |
| `sort_dir` | enum(asc, desc) | no | `desc` |  |
| `filtering_depth` | enum(5000, 10000, 30000, 40000, 50000) | no | `5000` |  |
| `filters` | string | no |  | Majestic filter predicates, e.g. TrustFlow("gt","10") and NoFollow("eq","false"); dates yyyy-MM-dd |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "item": {
      "type": "string",
      "description": "Domain, subdomain, or full URL"
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
      "minimum": 1,
      "maximum": 50000
    },
    "from_offset": {
      "type": "integer",
      "default": 0,
      "minimum": 0,
      "description": "Paging offset"
    },
    "mode": {
      "type": "integer",
      "enum": [
        0,
        1
      ],
      "default": 0,
      "description": "0=include deleted links; 1=exclude deleted"
    },
    "show_domain_info": {
      "type": "boolean",
      "default": false,
      "description": "Add a referring-domain info table"
    },
    "max_source_urls_per_ref_domain": {
      "type": "integer",
      "enum": [
        -1,
        1,
        3,
        10
      ],
      "default": -1
    },
    "ref_domain": {
      "type": "string",
      "description": "Only top-10 backlinks from this referring domain"
    },
    "filter_topic": {
      "type": "string",
      "description": "Topical Trust Flow topic filter, e.g. 'Computers/Programming'"
    },
    "use_prefix_scan": {
      "type": "boolean",
      "default": false,
      "description": "Treat item as path prefix (example.com/blog*)"
    },
    "enable_sorting_filtering": {
      "type": "boolean",
      "default": false,
      "description": "Enable sort_by/filters + stats tables (+5000 analysis units)"
    },
    "sort_by": {
      "type": "string",
      "enum": [
        "AnchorText",
        "DateDeleted",
        "DomainCitationFlow",
        "DomainTrustFlow",
        "ExternalOutlinks",
        "FirstSeen",
        "InternalOutlinks",
        "LastSeen",
        "OutDomainsExternal",
        "SourceCitationFlow",
        "SourceTrustFlow",
        "SourceUrl",
        "TargetUrlLength",
        "TotalOutlinks"
      ],
      "description": "Requires enable_sorting_filtering"
    },
    "sort_dir": {
      "type": "string",
      "enum": [
        "asc",
        "desc"
      ],
      "default": "desc"
    },
    "filtering_depth": {
      "type": "integer",
      "enum": [
        5000,
        10000,
        30000,
        40000,
        50000
      ],
      "default": 5000
    },
    "filters": {
      "type": "string",
      "description": "Majestic filter predicates, e.g. TrustFlow(\"gt\",\"10\") and NoFollow(\"eq\",\"false\"); dates yyyy-MM-dd"
    }
  },
  "required": [
    "item"
  ]
}
```

## Example request

```json
{
  "item": "majestic.com"
}
```

## Output

DataTables.BackLinks rows + headers (TotalBackLinks, AvailableLines)

Key fields: `DataTables.BackLinks.Data[].SourceURL`, `DataTables.BackLinks.Data[].AnchorText`, `DataTables.BackLinks.Data[].SourceTrustFlow`, `DataTables.BackLinks.Data[].FlagNoFollow`, `DataTables.BackLinks.Headers.TotalBackLinks`

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

- Need >50k links? Use the majestic_download_back_links job flow
- sort_by/filters silently do nothing without enable_sorting_filtering=True — the wrapper rejects that combination

## Alternatives

- `dataforseo_bl_list`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
