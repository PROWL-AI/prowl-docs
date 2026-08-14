# Scheduling & webhooks

A schedule runs an analysis without you asking each time. Two kinds: on an interval, or
when something on your side fires a webhook.

## Creating one

```json
{
  "tool": "prowl_schedule_create",
  "query": "backlink movement for example.com",
  "execution_mode": "basic",
  "interval_hours": 24
}
```

`execution_mode` is stored with the schedule and always explicit — a schedule never
picks a tier for you, because a tier picked automatically is a hold placed
automatically. It defaults to `basic` when you omit it.

Manage them with `prowl_schedule_list`, `prowl_schedule_pause`,
`prowl_schedule_resume` and `prowl_schedule_cancel`.

## Webhook-triggered runs

A schedule can be triggered by a request instead of a clock — useful when the thing that
should start a run happens in your system, not on a timer.

Triggering returns:

| Status | Meaning |
|---|---|
| `202` | accepted; the run is queued and proceeds asynchronously |
| `404` | no schedule for that token — usually a cancelled one |
| `429` | over **6** triggers per minute for this token |
| `503` | the run could not be queued; retry |

`202` means queued, not finished. Poll the session, or wait for the run to appear in
`prowl_schedule_list`.

**The token is the capability.** There is no request signature: whoever holds the URL can
trigger the run, and the run costs money. Treat it like a key — keep it server-side,
rotate by cancelling and re-creating the schedule.

## What a scheduled run costs

The same as the equivalent `prowl_analyze` at that tier, debited from the same wallet.
A schedule with no balance behind it does not run; it reports the failure rather than
silently skipping.

If the wallet cannot cover the hold for the stored tier, the run steps down to what the
balance can hold and logs that it did — same rule as an interactive run.

## Choosing an interval

Most market data does not move hourly. Backlink profiles and keyword volumes update on
the order of days; ad creative and SERP positions move faster. An interval shorter than
the data's own refresh rate spends money to re-read the same numbers.

A daily schedule on `basic` is the usual starting point. Move to `deep` when you need the
verification pass rather than the reading.
