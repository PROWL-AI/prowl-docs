# Troubleshooting

Ordered by how often each one is the actual cause.

## The client shows no tools

**The header is missing or malformed.** Prowl answers `401` with a `WWW-Authenticate`
header, and most clients render that as "no tools" rather than as an auth failure. The
header must be exactly `Authorization: Bearer prowl_<key>` — a bare key with no `Bearer`
is the most common version of this.

**The client did not reload.** Cursor and most IDE clients read MCP config at startup.
Reload the window after editing it.

**The transport is wrong.** Prowl is streamable HTTP, not stdio. A client configured to
launch a command will sit there failing to launch one.

## Everything returns 403

Authenticated, not allowed. Almost always an empty wallet — check the balance in the
dashboard. It can also mean a tier your account has no entitlement for; ask for `basic`
and see whether the same call works.

## Everything returns 429

You are over **120** requests per minute on that key.
Honour `Retry-After` if it is there. If you are driving many calls from a loop, consider
whether one `prowl_analyze` would do the same work in one request — see
[rate limits](../rate-limits.md).

## A tool call fails but others work

Read that tool's page in [the catalog](../tools/README.md): it lists the exact error
codes that tool returns and what each one means. The frequent ones are a missing
required parameter (`validation`) and a target that is not in that provider's index
(`not_found` — try a bare root domain rather than a full URL).

`prowl_get_error_feed` shows recent failures on your account with their causes, which
separates "my parameters changed" from "a provider is down" without guessing.

## A report never finishes

Reports take minutes. A blocking `prowl_analyze` holds the connection open for the whole
run and some clients give up first — that looks like a hang and is a client timeout.

Use the async shape instead: `prowl_start_session`, then poll `prowl_session_status`.
The run continues regardless of whether anything is watching it, and a queued run is
waiting rather than lost.

## The report used a smaller tier than I asked for

Deliberate, and it is reported rather than silent. If the balance could not cover the
hold for the tier that was picked, Prowl steps down to the highest tier the wallet can
actually hold — the alternative is refusing to run at all. Top up and re-run to get the
tier you asked for.

## An artifact was not generated

`prowl_analyze` writes a report. It does not produce a PDF, a deck, a video, an
infographic or audio — those come from a separate `prowl_generate_artifact` or
`prowl_export_report` call against the same `session_id`, and they are billed
separately. See [exports & artifacts](../guides/exports-and-artifacts.md).

## Nothing above

Open an issue with the request, the error object verbatim, and the time it happened.
Redact the key.
