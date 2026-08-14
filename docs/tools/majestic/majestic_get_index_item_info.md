---
name: majestic_get_index_item_info
provider: Majestic
provider_slug: majestic
category: seo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `majestic_get_index_item_info`

Majestic flagship: batch summary metrics for up to 100 domains/subdomains/URLs — TrustFlow, CitationFlow, ExtBackLinks, RefDomains, topical Trust Flow, crawl status, and the Ana...

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Majestic |
| Category | `seo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `discovery` |
| Tags | `majestic`, `seo` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "majestic_get_index_item_info",
  "params": {
    "items": [
      "majestic.com"
    ]
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `items` | string[] | yes |  | Domains / subdomains / full URLs to profile (batch up to 100) |
| `datasource` | enum(fresh, historic) | no | `fresh` | Majestic index: 'fresh' (recent, updated daily) or 'historic' (5+ years of data) |
| `desired_topics` | integer | no | `3` | Topical Trust Flow topics per item (max 30 domain / 20 subdomain / 10 URL) |
| `add_all_topics` | boolean | no | `False` | Include the full TrustCategories column |
| `enable_resource_unit_failover` | boolean | no | `False` | Bill Analysis/Retrieval units when IndexItemInfo units are exhausted |

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
      "maxItems": 100,
      "description": "Domains / subdomains / full URLs to profile (batch up to 100)"
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
    "desired_topics": {
      "type": "integer",
      "default": 3,
      "minimum": 0,
      "maximum": 30,
      "description": "Topical Trust Flow topics per item (max 30 domain / 20 subdomain / 10 URL)"
    },
    "add_all_topics": {
      "type": "boolean",
      "default": false,
      "description": "Include the full TrustCategories column"
    },
    "enable_resource_unit_failover": {
      "type": "boolean",
      "default": false,
      "description": "Bill Analysis/Retrieval units when IndexItemInfo units are exhausted"
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
    "majestic.com"
  ]
}
```

## Output

Envelope + DataTables.Results rows (one per item)

Key fields: `DataTables.Results.Data[].TrustFlow`, `DataTables.Results.Data[].CitationFlow`, `DataTables.Results.Data[].ExtBackLinks`, `DataTables.Results.Data[].RefDomains`, `DataTables.Results.Data[].Status`, `DataTables.Results.Data[].DownloadBacklinksAnalysisResUnitsCost`

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

- Status=MayExist rows are estimates, not confirmed index entries
- Use this before majestic_download_back_links to read the job's unit cost
- Cross-check backlink counts against dataforseo_bl_summary for evidence verification

**Chain groups:** `majestic`

## Alternatives

- `dataforseo_bl_summary`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://developer-support.majestic.com/api/commands/
