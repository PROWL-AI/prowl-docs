---
name: save_report_to_file
provider: Project Utility
provider_slug: project_utility
category: utility
generated_at: 2026-08-14T20:43:11Z
sources: [tool_defs, tool_bank, tool_profiles]
---

# `save_report_to_file`

Save data (dict/list/string) to a JSON file on disk.

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
  "tool_name": "save_report_to_file",
  "params": {
    "data": {
      "summary": "example"
    },
    "filename": "reports/example/note.json"
  }
}
```

`params` takes the object described under **Input**. Your wallet is debited per call at the price the [live catalog](https://prowl.chat) shows for this tool.

## Input

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `data` | object | yes |  | Data to save (will be JSON-serialized) |
| `filename` | string | yes |  | Relative path under reports/ (e.g. 'reports/domain/analysis.json'). Absolute paths and '..' segments are rejected for safety. |

### JSON Schema

```json
{
  "type": "object",
  "properties": {
    "data": {
      "type": "object",
      "description": "Data to save (will be JSON-serialized)"
    },
    "filename": {
      "type": "string",
      "description": "Relative path under reports/ (e.g. 'reports/domain/analysis.json'). Absolute paths and '..' segments are rejected for safety."
    }
  },
  "required": [
    "data",
    "filename"
  ]
}
```

## Example request

```json
{
  "data": {
    "summary": "example"
  },
  "filename": "reports/example/note.json"
}
```

## Output

Confirmation with saved file path

Key fields: `saved_to`, `filename`

## Errors

_Actions below that name a provider credential are ours to fix, not yours — see [errors](../../errors.md) for what each class means for a caller._

| Code | Meaning | Action |
|------|---------|--------|
| validation | Missing or invalid required argument | Fix the input and retry; check the tool's input_schema |
| io | Local filesystem or cache operation failed | Retry once; if it persists, skip the utility step and continue the hunt |
| path_rejected | Absolute path, '..' traversal, or unsafe filename rejected by safe_report_path | Use a relative path under reports/ only (e.g. 'reports/target/note.json') |

## When to use

- Only use when the user EXPLICITLY asks to save or export results to a file
- Do NOT include in plans by default — the report is delivered to the user on screen
- Saves to JSON files (e.g. 'reports/domain/analysis.json')

**Chain groups:** `utility`

## Alternatives

_None listed._
