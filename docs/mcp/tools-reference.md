# MCP tools reference

Connecting an agent to `https://prowl.chat/mcp` registers **22** tools (20 logical plus 2 legacy aliases kept for clients that already call them). These are the tools your agent sees. They are not the same thing as the **448** underlying API tools, which are reached *through* `prowl_call_tool` and are documented under [`../tools/`](../tools/README.md).

| Tool | What it does |
|---|---|
| `prowl_analyze` | Run a full research pass and compose a report. Accepts an optional `playbook_id` to force a fixed report shape. |
| `prowl_call_tool` | Invoke one underlying API tool directly, metered against your wallet. |
| `prowl_export_report` | Export a cached report in another format. |
| `prowl_generate_artifact` | Produce an artifact from a cached report. |
| `prowl_get_error_feed` | Recent errors on this account, with their causes. |
| `prowl_get_session` | A finished session's report and metadata. |
| `prowl_get_stats` | Usage and spend for this account. |
| `prowl_get_tool_info` | Legacy alias of `prowl_tool_info`. |
| `prowl_list_playbooks` | The persona-tuned report shapes available to `prowl_analyze`. |
| `prowl_list_sessions` | Sessions on this account. |
| `prowl_list_tools` | The underlying API tools, paged. |
| `prowl_reset_session` | Clear a session's conversation state and report cache. |
| `prowl_schedule_cancel` | Cancel a schedule. |
| `prowl_schedule_create` | Create a recurring or webhook-triggered run. |
| `prowl_schedule_list` | Schedules on this account. |
| `prowl_schedule_pause` | Pause a schedule. |
| `prowl_schedule_resume` | Resume a paused schedule. |
| `prowl_search_tools` | Semantic search across the tool bank. |
| `prowl_session_status` | Progress of an async run. |
| `prowl_start_session` | Start an analysis asynchronously and return a session id to poll. |
| `prowl_test_tool` | Legacy alias of `prowl_call_tool`. |
| `prowl_tool_info` | One tool's schema, cost basis and usage notes. |

## Calling an underlying tool

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_bl_summary",
  "params": {
    "target": "example.com"
  }
}
```

`params` is the object described on that tool's page. Arguments are **flat** — Prowl's MCP tools take no nested argument object.
