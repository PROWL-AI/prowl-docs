---
name: dataforseo_merchant_google_sellers
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_merchant_google_sellers`

Get sellers for a Google Shopping product — compare prices, shipping, and offers across retailers.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `dataforseo`, `google` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_merchant_google_sellers",
  "params": {
    "product_id": "B08N5WRWNW"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `additional_specifications` | string | no |  | object containing additional url parameters |
| `data_docid` | string | no |  | unique identifier of the SERP data element |
| `depth` | integer | no |  | parsing depth |
| `get_shops_on_google` | boolean | no |  | include “buy on Google” shops |
| `gid` | string | no |  | global product identifier on Google Shopping |
| `language_code` | string | no |  | language code |
| `location_code` | integer | no |  | location code |
| `location_coordinate` | string | no |  | GPS coordinates of a location |
| `pingback_url` | string | no |  | notification URL of a completed task |
| `postback_data` | string | no |  | postback_url datatype |
| `postback_url` | string | no |  | URL for sending task results |
| `priority` | integer | no |  | task priority |
| `pvf` | string | no |  | product variant filter on Google Shopping |
| `se_domain` | string | no |  | search engine domain |
| `tag` | string | no |  | user-defined task identifier |
| `product_id` | string | yes |  | Google Shopping product ID |
| `location_name` | string | no |  | Full location name (e.g. 'United States', 'London,England,United Kingdom') |
| `language_name` | string | no |  | Full language name (e.g. 'English', 'German') |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "additional_specifications": {
      "type": "string",
      "description": "object containing additional url parameters"
    },
    "data_docid": {
      "type": "string",
      "description": "unique identifier of the SERP data element"
    },
    "depth": {
      "type": "integer",
      "description": "parsing depth"
    },
    "get_shops_on_google": {
      "type": "boolean",
      "description": "include \u201cbuy on Google\u201d shops"
    },
    "gid": {
      "type": "string",
      "description": "global product identifier on Google Shopping"
    },
    "language_code": {
      "type": "string",
      "description": "language code"
    },
    "location_code": {
      "type": "integer",
      "description": "location code"
    },
    "location_coordinate": {
      "type": "string",
      "description": "GPS coordinates of a location"
    },
    "pingback_url": {
      "type": "string",
      "description": "notification URL of a completed task"
    },
    "postback_data": {
      "type": "string",
      "description": "postback_url datatype"
    },
    "postback_url": {
      "type": "string",
      "description": "URL for sending task results"
    },
    "priority": {
      "type": "integer",
      "description": "task priority"
    },
    "pvf": {
      "type": "string",
      "description": "product variant filter on Google Shopping"
    },
    "se_domain": {
      "type": "string",
      "description": "search engine domain"
    },
    "tag": {
      "type": "string",
      "description": "user-defined task identifier"
    },
    "product_id": {
      "type": "string",
      "description": "Google Shopping product ID"
    },
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'United States', 'London,England,United Kingdom')"
    },
    "language_name": {
      "type": "string",
      "description": "Full language name (e.g. 'English', 'German')"
    }
  },
  "required": [
    "product_id"
  ]
}
```

## Example request

```json
{
  "product_id": "B08N5WRWNW"
}
```

## Output

Get sellers for a Google Shopping product — compare prices, shipping, and offers across retailers.

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing credentials | Check DATAFORSEO_LOGIN and DATAFORSEO_PASSWORD env vars |
| 402 | Insufficient balance | Top up DataForSEO account balance |
| 429 | Rate limit exceeded | Wait 10s and retry once |
| 500 | Server error | Retry after 30s; skip tool if persistent |

## When to use

- DataForSEO live calls bill per request — prefer Labs domain/keyword endpoints over full SERP scrapes when comparing domains
- Pass location_code + language_name (or language_code) for geo-correct volumes; defaults skew US/English
- Async/task endpoints need task_id follow-up; live endpoints return tasks[].result in one call

- Chain dependency: obtain `product_id` from `dataforseo_merchant_google_products` first, then pass it here.
- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

**Chain inputs:** `{'param': 'product_id', 'from_tool': 'dataforseo_merchant_google_products', 'extract': '_custom_dfs_product_id'}`

**Chain groups:** `dataforseo_merchant`

## Alternatives

- `dataforseo_merchant_google_products`
- `dataforseo_app_google_info`
- `dataforseo_app_google_searches`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
