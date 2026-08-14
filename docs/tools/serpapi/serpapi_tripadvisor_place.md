---
name: serpapi_tripadvisor_place
provider: SerpAPI
provider_slug: serpapi
category: serpapi_serp
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `serpapi_tripadvisor_place`

Tripadvisor place details via SerpAPI.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | SerpAPI |
| Category | `serpapi_serp` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `dependent` |
| Tags | `ads`, `places`, `serp`, `serpapi`, `serpapi_serp` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `FAIL` — 2026-08-13T17:14:24.497438 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "serpapi_tripadvisor_place",
  "params": {
    "data_id": "data_id_example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `data_id` | string | yes |  | Tripadvisor data_id from search results |
| `tripadvisor_domain` | string | no |  | Regional Tripadvisor site, e.g. 'www.tripadvisor.co.uk'. Use the SAME domain the data_id was found on — otherwise you read the place back in another language and review set. SerpApi requires the www. prefix; it is added for you if omitted. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "data_id": {
      "type": "string",
      "description": "Tripadvisor data_id from search results"
    },
    "tripadvisor_domain": {
      "type": "string",
      "description": "Regional Tripadvisor site, e.g. 'www.tripadvisor.co.uk'. Use the SAME domain the data_id was found on \u2014 otherwise you read the place back in another language and review set. SerpApi requires the www. prefix; it is added for you if omitted."
    }
  },
  "required": [
    "data_id"
  ]
}
```

## Example request

```json
{
  "data_id": "data_id_example"
}
```

## Output

Tripadvisor place details via SerpAPI.

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| 401 | Invalid or missing SERP_API_KEY | Check SERP_API_KEY in .env or SerpAPI dashboard |
| 429 | Monthly rate limit reached | Upgrade SerpAPI plan or wait for quota reset |
| 400 | Missing required parameters | Check query and engine parameters |

## When to use

- SerpAPI engine is encoded in the tool name — do not re-pass engine unless the schema requires it
- Prefer the SearchAPI twin when cost/coverage is better for the same surface
- Paginate with num/start (or page) when result sets are truncated

- Chain dependency: obtain `data_id` from `serpapi_tripadvisor` first, then pass it here.
- Chain-dependent: success-shaped live capture needs upstream IDs/steps (product id, board id, place id, portal filters, or healthy sub-providers). Not a missing handler — mark chain_dependent so docs completeness skips penalty.

**Chain inputs:** `{'param': 'data_id', 'from_tool': 'serpapi_tripadvisor', 'extract': '_custom_tripadvisor_id'}`

**Chain groups:** `serpapi_places`

## Alternatives

- `serpapi_tripadvisor`
- `serpapi_yelp_place`
- `serpapi_amazon`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://serpapi.com/search-api
