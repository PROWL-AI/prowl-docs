---
name: foreplay_get_board_brands
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_get_board_brands`

Get all brands in a specific Foreplay board.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Foreplay |
| Category | `ads` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `foreplay` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_get_board_brands",
  "params": {
    "board_id": "board_example_001"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `board_id` | string | yes |  | Board ID from foreplay_get_boards |
| `offset` | integer | no | `0` | Pagination offset (default: 0) |
| `limit` | integer | no | `10` | Max brands |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "board_id": {
      "type": "string",
      "description": "Board ID from foreplay_get_boards"
    },
    "offset": {
      "type": "integer",
      "description": "Pagination offset (default: 0)",
      "default": 0
    },
    "limit": {
      "type": "integer",
      "description": "Max brands",
      "default": 10,
      "minimum": 1,
      "maximum": 10
    }
  },
  "required": [
    "board_id"
  ]
}
```

## Example request

```json
{
  "board_id": "board_example_001"
}
```

## Output

Brands in the board

Key fields: `data[].id`, `data[].name`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use board ID from foreplay_get_boards to list brands in that board
- Follow up with foreplay_get_ads_by_brand_ids to get ad creatives for those brands

- Chain dependency: obtain `board_id` from `foreplay_get_boards` first, then pass it here.
- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

**Chain inputs:** `{'param': 'board_id', 'from_tool': 'foreplay_get_boards', 'extract': 'data[].id'}`

**Chain groups:** `foreplay`

## Alternatives

_None listed._

## Provider docs

https://docs.foreplay.co
