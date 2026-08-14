# Errors

Prowl speaks JSON-RPC over MCP, so a failure arrives as an error object with a code.
Four codes cover the transport; everything else is a tool telling you what it could not
do.

## Transport codes

| Code | HTTP | Meaning | Do |
|---|---|---|---|
| `-32001` | 401 | not authenticated | check the `Authorization` header and that the key is not revoked |
| `-32002` | 429 | rate limited | honour `Retry-After`; see [rate limits](rate-limits.md) |
| `-32003` | 403 | authenticated, not allowed | usually an empty wallet or a tier you have no entitlement for |
| `-32603` | 500 / 503 | Prowl failed | retry with backoff; if it persists, `prowl_get_error_feed` has the cause |

`-32003` is the one people misread. It does not mean the key is wrong — it means the key
is right and the request still may not proceed. An empty wallet is the common cause.

## Tool errors

A tool call that reaches its provider and fails returns a structured error rather than a
transport code. Each tool's page lists its own table; the shapes recur:

| Class | Typical cause | Do |
|---|---|---|
| `validation` | a required parameter is missing or malformed | read the tool's input schema; `prowl_tool_info` returns it |
| `invalid_api_key` | the provider rejected our credential | not yours to fix — report it, we will see it too |
| `insufficient_credits` | the provider's own quota is exhausted | retry later, or use an alternative tool named on the page |
| `rate_limit` | the provider throttled us | retry with backoff; the pool already paces concurrency |
| `not_found` | the target is not in that provider's index | try a different index, or a bare root domain instead of a URL |
| `timeout` | the provider did not answer in time | retry; some endpoints are task-based and genuinely slow |

Every tool page in [the catalog](tools/README.md) carries the exact codes that tool can
return, what each means, and the action for it.

## Seeing what happened

`prowl_get_error_feed` returns recent failures on your account with their causes. It is
the first thing to call when something worked yesterday and does not today — it
distinguishes "your parameters changed" from "a provider is down" without guessing.

## Failures that are not errors

- **A report that says it could not verify a claim** is working correctly. Refuted
  claims ship in an appendix rather than being dropped.
- **A tier that was lowered** is reported, not silent: if the wallet could not cover the
  hold for the tier that was picked, the run says which tier it actually used.
- **A queued run** is not a failed one. Poll it.
