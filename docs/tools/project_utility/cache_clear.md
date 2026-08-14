---
name: cache_clear
provider: Project Utility
provider_slug: project_utility
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `cache_clear`

Clear the API response cache.

## Quick facts

| Field | Value |
|-------|-------|
| Provider | Project Utility |
| Category | `utility` |
| Timeout | _default_ |
| Blocking | `False` |
| Chain role | `standalone` |
| Tags | `project-utility`, `utility` |
| Last schema check | `PASS` — 2026-08-10T20:44:23Z |
| Last live API check | `SKIP` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "cache_clear",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `func_name` | string | no |  | Optional: name of the API function to clear cache for (e.g. 'discovery_brands', 'get_domain_stats_for_n_months'). Omit to clear all cached responses. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "func_name": {
      "type": "string",
      "description": "Optional: name of the API function to clear cache for (e.g. 'discovery_brands', 'get_domain_stats_for_n_months'). Omit to clear all cached responses."
    }
  }
}
```

## Example request

```json
{}
```

## Output

Confirmation with count of deleted entries

Key fields: `cleared`, `entries_deleted`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| validation | Missing or invalid required argument | Fix the input and retry; check the tool's input_schema |
| io | Local filesystem or cache operation failed | Retry once; if it persists, skip the utility step and continue the hunt |

## When to use

- Clears cached API responses — all or by function name
- Use when you need fresh data from an API that may have changed

## Alternatives

_None listed._
