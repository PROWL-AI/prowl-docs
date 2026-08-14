# Rate limits

The numbers, then what to do when you hit one.

| Surface | Limit | Scope |
|---|---|---|
| MCP calls | **120** / minute | per API key |
| MCP, before authentication | **300** / minute | per IP |
| Login | **10** / minute | per account |
| Registration | **5** / hour | per IP |
| Billing endpoints | **5** / minute | per account |
| Schedule webhooks | **6** / minute | per webhook token |

The pre-auth IP limit is higher than the per-key one on purpose: it exists to absorb
noise before a request has an identity, not to shape legitimate traffic.

## When you hit one

You get `429`. If the response carries `Retry-After`, honour it — that is the real
answer and it beats any backoff you compute. Without it, back off exponentially from a
second, with jitter, and cap at a minute.

What not to do: retry immediately in a loop. A limiter that keeps being hit stays hit,
and a tight retry loop turns one slow minute into a long one.

## Concurrency

Reports are a separate constraint from request rate. An account runs a bounded number of
analyses at once; beyond that, runs queue rather than fail. A queued run is not a lost
run — poll it with `prowl_session_status`.

For anything long, prefer the async shape: `prowl_start_session`, then poll. A blocking
`prowl_analyze` holds a connection open for minutes, and some clients give up before
Prowl does.

## Designing around the limits

- **Batch through a report, not through a loop.** One `prowl_analyze` plans and runs its
  own graph of calls; it is cheaper in requests than the same work driven call by call
  from your side.
- **Search once, call many.** `prowl_search_tools` finds the tool; you do not need to
  re-search per call.
- **Cache on your side.** Backlink summaries and keyword volumes do not change by the
  minute, and Prowl bills every call whether or not you asked the same question an hour
  ago.
