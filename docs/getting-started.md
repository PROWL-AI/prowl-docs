# Getting started

Three steps, in order. The whole thing takes about five minutes, and the third one
costs a few cents.

## 1. Get a key

Sign up at [https://prowl.chat](https://prowl.chat) and create an API key from the dashboard. It looks like
`prowl_` followed by a random string. A new account starts with free credit, which is
enough to run several direct tool calls and one small report.

Treat the key as a password: it authenticates and it spends. Put it in an environment
variable or a git-ignored file, never in a committed config.

## 2. Connect your agent

Point your MCP client at:

```
https://prowl.chat/mcp
```

with the header `Authorization: Bearer prowl_<your_key>`. Per-client configuration —
Cursor, Claude Code, Codex, and a generic client — is in
[client setup](mcp/client-setup.md).

Verify the connection by asking your agent to list the tools. You should see
**22** of them.

## 3. Make a call

Two things you can do, and they are different in cost and in kind.

**Call one tool.** Cheap, fast, exact — you get the provider's data back.

```json
{
  "tool": "prowl_call_tool",
  "tool_name": "dataforseo_bl_summary",
  "params": { "target": "example.com" }
}
```

Find the tool you want with `prowl_search_tools`, or browse
[the catalog](tools/README.md). Every page carries the input schema, an example
request and the error table.

**Run a report.** Prowl plans a graph of tool calls, executes it, verifies the claims
against independent tools, and writes a structured report.

```json
{
  "tool": "prowl_analyze",
  "query": "competitive landscape for example.com in the US",
  "execution_mode": "basic"
}
```

This takes minutes, not seconds, and it costs materially more than a single call — see
[billing](billing.md) for the ceiling per tier and [your first report](guides/first-report.md)
for what to expect while it runs.

## What to read next

- [Billing](billing.md) — how the wallet works before you spend from it
- [Rate limits](rate-limits.md) — **120** requests per minute per key
- [Errors](errors.md) — what each failure means
