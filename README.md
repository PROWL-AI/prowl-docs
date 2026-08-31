# Prowl documentation

**The market intelligence connector for AI agents.** One MCP endpoint gives any
agent — Cursor, Claude Code, Codex, or your own stack — **447** market
data tools across **17** providers: SEO, backlinks, paid ads, SERP,
app stores, reviews, web scraping and LLM-mention tracking. Billed per call against
one USD wallet.

Your agent already reasons. It just has no market data.

```
Endpoint   https://prowl.chat/mcp
Auth       Authorization: Bearer prowl_<your_key>
Tools      23 registered (21 logical + legacy aliases)
Underneath 447 API tools reachable through prowl_call_tool
```

## Start here

| | |
|---|---|
| [Getting started](docs/getting-started.md) | Key → connect → first call, in that order |
| [Client setup](docs/mcp/client-setup.md) | Cursor, Claude Code, Codex, and a generic MCP client |
| [MCP tools reference](docs/mcp/tools-reference.md) | The 23 tools your agent sees |
| [Tool catalog](docs/tools/README.md) | All 447 underlying tools, one page each |

## Then

| | |
|---|---|
| [Authentication](docs/authentication.md) | API keys and OAuth 2.1 |
| [Billing](docs/billing.md) | The wallet, tiers, holds, and what a run actually costs |
| [Rate limits](docs/rate-limits.md) | The numbers, and how to back off |
| [Errors](docs/errors.md) | Every code, what it means, what to do |
| [Your first report](docs/guides/first-report.md) | What `prowl_analyze` does and how long it takes |
| [Scheduling & webhooks](docs/guides/scheduling-and-webhooks.md) | Recurring runs and triggers |
| [Exports & artifacts](docs/guides/exports-and-artifacts.md) | The 5 artifact types, and when they cost extra |
| [Playbooks](docs/guides/playbooks.md) | Forcing a fixed report shape |
| [Troubleshooting](docs/mcp/troubleshooting.md) | It connected but nothing works |

## What Prowl reports about itself

A report's claims are extracted, cross-checked against independent tools, and the
refuted ones ship in an appendix rather than disappearing. Every report opens by
naming the market it resolved and how — stated by the caller, inferred from the
request, or assumed. When a number could not be verified, the report says so.

That disclosure is not a disclaimer at the end. It is the reason to trust the other
numbers.

## About this repository

Generated from the Prowl codebase and pushed on every release, so what you read here
is what the endpoint currently serves — including the tool schemas, which are rendered
from the live registry rather than transcribed. [`CHANGELOG.md`](CHANGELOG.md) records
what changed in the API itself: tools added, removed or renamed, parameters that became
required, new error codes.

Found something wrong? Open an issue here. Corrections land in the generator, not in
the published file — a fix applied to the output would be overwritten by the next sync.

Prices are deliberately absent from the tool pages: they are runtime configuration, so
any figure committed to a file would be stale. The live catalog at
[https://prowl.chat](https://prowl.chat) shows what a call costs.
