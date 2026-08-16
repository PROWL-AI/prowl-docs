# Prowl REST API v1

Wallet, usage, tool catalog and API keys for agents using Prowl.

The REST surface an agent uses to watch what it is spending.

Prowl's product surface is the MCP endpoint at `https://prowl.chat/mcp`, where an agent
gains 448 market-intelligence tools and every call is metered against a prepaid USD
wallet. This API is the other half of that arrangement: read the balance, read what each
call cost, and manage the keys that authorise them.

Authentication is a bearer token — either a JWT from sign-in or a `prowl_...` API key
generated in MCP Home. Two operations need no credential at all, because a price list
that demands a key cannot be compared before you buy: `GET /api/v1/tools/pricing` and
`GET /api/v1/tools/catalog`.

The machine-readable description of everything below is [`openapi.json`](./openapi.json), also served live at <https://prowl.chat/openapi.json>. Discovery from the site root works through `/.well-known/api-catalog` (RFC 9727) and the `Link` response header.

## Endpoints

### `GET /api/v1/keys`

**List API keys** — Every key on the account with its scope, limits and last use. Secrets are never returned — only the prefix, which is enough to tell two keys apart.

- Operation id: `getKeys`
- Bearer token required

### `POST /api/v1/keys`

**Create an API key** — Mints a `prowl_...` key, optionally scoped to categories, spend limits and an IP allowlist. **The secret is returned once and is never retrievable again** — store it when you receive it.

- Operation id: `createKeys`
- Bearer token required

### `DELETE /api/v1/keys/{key_id}`

**Revoke an API key** — Takes effect immediately: the next call presenting this key fails authentication. Revoking the key behind an OAuth connector kills that connector too, without touching the OAuth grant.

- Operation id: `revokeKeys`
- Bearer token required

### `GET /api/v1/tools/catalog`

**Browse the full tool catalog** — Every registered tool with what it does, who runs it, what it costs and where its documentation lives. No credential required. This is the endpoint to read when choosing which tool answers a question.

- Operation id: `getToolsCatalog`
- No credential required

### `GET /api/v1/tools/health`

**Read per-tool health** — Success rate and latest outcome per tool over a recent window, aggregated across all callers — no per-user data. A tool missing from the reply had no calls in the window, which reads as idle rather than broken.

- Operation id: `getToolsHealth`
- Bearer token required

### `GET /api/v1/tools/pricing`

**Read the public price list** — What each tool costs to call, with no credential required — a price you cannot read before signing up is a price you cannot compare. Returns what a call debits from your wallet, and nothing about how that figure is arrived at.

- Operation id: `getToolsPricing`
- No credential required

### `GET /api/v1/usage/summary`

**Summarise spend over a window** — Spend rolled up over the last `days` days — totals, the twenty tools that cost the most, and the current balances alongside them so a budget decision needs one request rather than two.

- Operation id: `getUsageSummary`
- Bearer token required

### `GET /api/v1/usage/tools`

**List recent metered calls (alias)** — Identical to `GET /api/v1/wallet/invocations`; kept because usage and wallet are two words for the same question and clients reach for both.

- Operation id: `getUsageTools`
- Bearer token required

### `GET /api/v1/wallet`

**Read wallet balances** — Returns the two pools a call is paid from: plan credit, which burns at the end of the billing period and is spent first, and top-up credit, which never expires. Figures are rounded to whole cents at this boundary.

- Operation id: `getWallet`
- Bearer token required

### `GET /api/v1/wallet/invocations`

**List recent metered calls** — Every tool call this account has been billed for, newest first, with what the provider charged and what the wallet was debited. Use it to reconcile a balance against the work that produced it.

- Operation id: `getWalletInvocations`
- Bearer token required
