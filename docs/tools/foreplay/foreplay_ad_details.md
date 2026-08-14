---
name: foreplay_ad_details
provider: Foreplay
provider_slug: foreplay
category: ads
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `foreplay_ad_details`

Get full details for a single ad by its ad_id from Foreplay.

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
| Last live API check | `PASS` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "foreplay_ad_details",
  "params": {
    "ad_id": "ad_example_001"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `ad_id` | string | yes |  | The ad ID to fetch details for |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "ad_id": {
      "type": "string",
      "description": "The ad ID to fetch details for"
    }
  },
  "required": [
    "ad_id"
  ]
}
```

## Example request

```json
{
  "ad_id": "ad_example_001"
}
```

## Output

Complete ad data with all creative variations

Key fields: `ad_id`, `type`, `cards`, `transcription`, `headlines`, `descriptions`, `ctas`, `targeting`, `emotional_drivers`, `running_duration`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing FOREPLAY_AD_SPY_API | Skip Foreplay tools — use meta_ad_library from SearchAPI as alternative |
| 429 | Rate limit exceeded | Wait 60s and retry once |
| 400 | Bad request or excluded domain | Check input params; for brands_by_domain, domain may be blocked by Foreplay |

## When to use

- Use to get full details of a specific ad creative by its ID
- Includes transcription, targeting, emotional drivers, and all creative variations

**Chain inputs:** `{'param': 'ad_id', 'from_tool': 'foreplay_discovery_ads', 'extract': 'data[].ad_id'}`

**Chain groups:** `foreplay`

## Alternatives

_None listed._

## Provider docs

https://docs.foreplay.co
