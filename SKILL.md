---
name: prowl-docs
description: Reference for the Prowl MCP endpoint — connecting an agent, authenticating, what each of the 23 MCP tools does, and the input schema, example request and error table for every one of the 448 underlying market-intelligence tools (SEO, backlinks, paid ads, SERP, app stores, reviews, scraping, LLM-mention tracking). Use when wiring Prowl into an agent, choosing a tool for a market-data question, or debugging a Prowl call.
---

# Prowl MCP — reference

Prowl is one MCP endpoint that gives an agent **448** market data tools
across **17** providers, billed per call against a USD wallet.

```
Endpoint  https://prowl.chat/mcp
Auth      Authorization: Bearer prowl_<key>
Tools     23 registered (21 logical + legacy aliases)
```

## Deciding what to call

**A specific number** — one domain's backlinks, one keyword's volume, one competitor's
ad creative → call the tool directly.

```json
{ "tool": "prowl_call_tool", "tool_name": "<name>", "params": { } }
```

Find it with `prowl_search_tools` (semantic), confirm the schema with `prowl_tool_info`,
then call. Arguments are **flat** — no nested argument object.

**An open question** — a landscape, a positioning read, whether an idea has a market →
run a report.

```json
{ "tool": "prowl_analyze", "query": "…", "execution_mode": "basic|deep|max" }
```

Reports take minutes and cost materially more than a single call. From a client that may
time out, use `prowl_start_session` and poll `prowl_session_status`.

## Things that are wrong more often than they should be

- **`prowl_analyze` produces no artifact.** PDF, deck, video, infographic and audio come
  from a separate, separately-billed `prowl_generate_artifact` call on the same
  `session_id`.
- **`prowl_call_tool` takes `params`, not `arguments`.**
- **A tier is a spending ceiling, not a price.** A run is billed what it spent, and never
  more than the hold placed before it.
- **One run is one market.** Country and language are resolved once and stated in the
  report's first line. Say the market in the query if it matters.
- **`-32003` is not a bad key.** It is an authenticated request that may not proceed —
  usually an empty wallet.

## Where the detail lives

| | |
|---|---|
| [`docs/mcp/tools-reference.md`](docs/mcp/tools-reference.md) | the 23 MCP tools |
| [`docs/tools/README.md`](docs/tools/README.md) | all 448 underlying tools, one page each |
| [`docs/mcp/client-setup.md`](docs/mcp/client-setup.md) | Cursor, Claude Code, Codex, generic |
| [`docs/errors.md`](docs/errors.md) | every code and its action |
| [`docs/billing.md`](docs/billing.md) | wallet, tiers, holds |
| [`docs/rate-limits.md`](docs/rate-limits.md) | 120/min per key |

Every tool page carries the input schema, an example request, the response shape, the
error table, the tools it chains with and its alternatives. Prices are not in this
repository — they are runtime configuration, and the live catalog at
[https://prowl.chat](https://prowl.chat) computes them.
