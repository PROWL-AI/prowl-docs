---
name: cache_stats
provider: Project Utility
provider_slug: project_utility
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `cache_stats`

Show API response cache statistics: total cached entries, hit counts, database size, and per-function breakdown.

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
| Last live API check | `PASS` — 2026-08-10T22:44:23.526138 |

## Call it

Connect an agent to `https://prowl.chat/mcp`, then:

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "cache_stats",
  "params": {}
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

_No parameters._

### JSON Schema

```json
{
  "type": "object",
  "properties": {}
}
```

## Example request

```json
{}
```

## Output

Cache statistics

Key fields: `total_entries`, `total_hits_db`, `db_size_mb`, `by_function`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| validation | Missing or invalid required argument | Fix the input and retry; check the tool's input_schema |
| io | Local filesystem or cache operation failed | Retry once; if it persists, skip the utility step and continue the hunt |

## When to use

- Shows API cache statistics — hits, size, per-function breakdown

## Alternatives

_None listed._
