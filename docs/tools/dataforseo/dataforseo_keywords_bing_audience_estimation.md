---
name: dataforseo_keywords_bing_audience_estimation
provider: DataForSEO
provider_slug: dataforseo
category: dataforseo
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `dataforseo_keywords_bing_audience_estimation`

Estimate the size of a Bing/LinkedIn audience reachable with given targeting criteria (location, age, gender, industry, job function) and a bid/daily budget.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | DataForSEO |
| Category | `dataforseo` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `dataforseo`, `keywords` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_keywords_bing_audience_estimation",
  "params": {
    "location_name": "example"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `location_name` | string | yes |  | Full location name (e.g. 'London,England,United Kingdom'). Required if location_code omitted. |
| `location_code` | integer | no |  | Location code (e.g. 2840). Required if location_name omitted. |
| `age` | any[] | no |  | Age range targeting. Possible values: eighteen_to_twenty_four, twenty_five_to_thirty_four, thirty_five_to_forty_nine, fifty_to_sixty_four, sixty_five_and_above, thirteen_to_seventeen, zero_to_twelve, unknown. |
| `gender` | any[] | no |  | Gender targeting. Possible values: male, female, unknown. |
| `bid` | number | no |  | Desired bid value in USD (max 1000). |
| `daily_budget` | number | no |  | Daily campaign budget in USD (max 10000). |
| `industry` | any[] | no |  | LinkedIn industry IDs for targeting. Retrieve valid IDs from /keywords_data/bing/audience_estimation/industries. |
| `job_function` | any[] | no |  | LinkedIn job function IDs for targeting. Retrieve valid IDs from /keywords_data/bing/audience_estimation/job_functions. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "location_name": {
      "type": "string",
      "description": "Full location name (e.g. 'London,England,United Kingdom'). Required if location_code omitted."
    },
    "location_code": {
      "type": "integer",
      "description": "Location code (e.g. 2840). Required if location_name omitted."
    },
    "age": {
      "type": "array",
      "description": "Age range targeting. Possible values: eighteen_to_twenty_four, twenty_five_to_thirty_four, thirty_five_to_forty_nine, fifty_to_sixty_four, sixty_five_and_above, thirteen_to_seventeen, zero_to_twelve, unknown."
    },
    "gender": {
      "type": "array",
      "description": "Gender targeting. Possible values: male, female, unknown."
    },
    "bid": {
      "type": "number",
      "description": "Desired bid value in USD (max 1000)."
    },
    "daily_budget": {
      "type": "number",
      "description": "Daily campaign budget in USD (max 10000)."
    },
    "industry": {
      "type": "array",
      "description": "LinkedIn industry IDs for targeting. Retrieve valid IDs from /keywords_data/bing/audience_estimation/industries."
    },
    "job_function": {
      "type": "array",
      "description": "LinkedIn job function IDs for targeting. Retrieve valid IDs from /keywords_data/bing/audience_estimation/job_functions."
    }
  },
  "additionalProperties": true,
  "description": "Parameters for the DataForSEO `keywords_data/bing/audience_estimation/live` live endpoint. Listed properties are the curated core; additional keys are accepted and forwarded verbatim to the endpoint (full field list: https://docs.dataforseo.com/v3/).",
  "required": [
    "location_name"
  ]
}
```

## Example request

```json
{
  "location_name": "example"
}
```

## Output

| Path | Type | Description |
|------|------|-------------|
| `[]` | array<object> |  |
| `[].est_impressions` | object |  |
| `[].est_impressions.high` | integer |  |
| `[].est_impressions.low` | integer |  |
| `[].est_audience_size` | object |  |
| `[].est_audience_size.high` | integer |  |
| `[].est_audience_size.low` | integer |  |
| `[].est_clicks` | object |  |
| `[].est_clicks.high` | integer |  |
| `[].est_clicks.low` | integer |  |
| `[].est_spend` | object |  |
| `[].est_spend.high` | integer |  |
| `[].est_spend.low` | integer |  |
| `[].est_cost_per_event` | object |  |
| `[].est_cost_per_event.high` | null |  |
| `[].est_cost_per_event.low` | null |  |
| `[].est_ctr` | object |  |
| `[].est_ctr.high` | number |  |
| `[].est_ctr.low` | integer |  |
| `[].suggested_bid` | null |  |
| `[].suggested_budget` | null |  |
| `[].events_lost_to_bid` | null |  |
| `[].events_lost_to_budget` | null |  |
| `[].est_reach_audience_size` | integer |  |
| `[].est_reach_impressions` | integer |  |

### Example response (from profile)

```json
[
  {
    "est_impressions": {
      "high": 17090000,
      "low": 4270000
    },
    "est_audience_size": {
      "high": 821400,
      "low": 352030
    },
    "est_clicks": {
      "high": 242540,
      "low": 60630
    },
    "est_spend": {
      "high": 1520000,
      "low": 80180
    },
    "est_cost_per_event": {
      "high": null,
      "low": null
    },
    "est_ctr": {
      "high": 0.028391361817436185,
      "low": 0
    },
    "suggested_bid": null,
    "suggested_budget": null,

...
```

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

## Alternatives

- `dataforseo_ai_keyword_volume`
- `dataforseo_labs_amazon_product_keyword_intersections`
- `dataforseo_labs_amazon_related_keywords`

_Full paths: [catalog index](../README.md)._

## Provider docs

https://docs.dataforseo.com/v3/
