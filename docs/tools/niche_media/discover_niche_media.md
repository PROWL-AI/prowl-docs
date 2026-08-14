---
name: discover_niche_media
provider: NicheMedia (composite: Exa + SearchAPI + Firecrawl)
provider_slug: niche_media
category: web
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `discover_niche_media`

Discover the niche media landscape for a topic/audience: newsletters, podcasts, communities (incl.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | NicheMedia (composite: Exa + SearchAPI + Firecrawl) |
| Category | `web` |
| Timeout | 180 |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `nichemedia-(composite:-exa-+-searchapi-+-firecrawl)`, `web` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "discover_niche_media",
  "params": {
    "topic": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `topic` | string | yes |  | The niche/topic to inventory (e.g. 'infrastructure monitoring') |
| `audience` | string | no |  | Optional audience qualifier (e.g. 'devops engineers') |
| `channel_types` | string[] | no |  | Channel types to include (default: all five) |
| `max_results` | integer | no | `15` | Max channels returned and max evidence scrapes (default 15, ceiling 30) |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "topic": {
      "type": "string",
      "description": "The niche/topic to inventory (e.g. 'infrastructure monitoring')"
    },
    "audience": {
      "type": "string",
      "description": "Optional audience qualifier (e.g. 'devops engineers')"
    },
    "channel_types": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "newsletter",
          "podcast",
          "community",
          "blog",
          "youtube"
        ]
      },
      "description": "Channel types to include (default: all five)"
    },
    "max_results": {
      "type": "integer",
      "description": "Max channels returned and max evidence scrapes (default 15, ceiling 30)",
      "default": 15
    }
  },
  "required": [
    "topic"
  ]
}
```

## Example request

```json
{
  "topic": "example"
}
```

## Output

Ranked niche-media channel inventory with evidence and degradation flags

Key fields: `channels`, `channels[].name`, `channels[].url`, `channels[].type`, `channels[].audience_estimate`, `channels[].audience_evidence`, `channels[].sponsorship_signals`, `channels[].contact`, `channels[].relevance`, `queries_used`, `degraded`, `dropped_count`, `cost_usd`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| RuntimeError: all N sub-provider calls failed | Exa, SearchAPI and YouTube search all errored — provider keys or upstream outage | Fall back to alternatives: exa_keyword_search / firecrawl_search |
| degraded=true in response | Some sub-calls failed or the 150s internal budget cut scrapes short; inventory is partial | Use the returned channels; dropped_count tells how many lookups were lost |

## When to use

- Use for distribution/channel research and idea validation — inventories where the audience already gathers
- Follow up with firecrawl_scrape_website on the most relevant channels to read their sponsor/media-kit pages

- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

## Alternatives

- `exa_keyword_search`
- `firecrawl_search`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.exa.ai / https://www.searchapi.io/docs / https://docs.firecrawl.dev
