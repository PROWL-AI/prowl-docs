# Billing

Prowl runs on a prepaid wallet in USD. You top it up, calls debit it, and nothing
auto-charges a card mid-run.

## Topping up

One-time credit packs through Stripe Checkout — **$10**, **$50** or **$200**, each
credited 1:1 to your balance. Card details are entered on Stripe's own hosted page;
Prowl never sees them. Receipts come from Stripe.

A declined card leaves the balance untouched and the checkout session unused; retry with
another card. Packs do not expire.

Subscriptions are separate and additive: a plan grants monthly credit on top of whatever
you top up, and unlocks the higher analysis tiers. Plan credit is a monthly pool that
resets; topped-up credit is yours until spent.

## What a call costs

**A direct tool call** — `prowl_call_tool` — is metered per call. The live catalog at
[https://prowl.chat](https://prowl.chat) shows the current price for each tool, computed at runtime; the
tool pages in this repository deliberately do not, because a number committed to a file
is stale the next time the multiplier moves.

**A report** — `prowl_analyze` — is the expensive one, because it is many tool calls
plus the language model that plans them and writes the result.

## Tiers and the hold

Every report runs at a tier, and the tier sets the ceiling on what it may spend with
providers:

| Tier | Provider-cost ceiling | What it is for |
|---|---|---|
| `basic` | $2.5 | a fast read on one question |
| `deep` | $8 | a full competitive pass, evidence verified |
| `max` | $18 | the widest sweep, most modules, most cross-checks |

That is a **ceiling, not a price**. A typical run costs less, and you are billed what it
actually spent.

Before a run starts, Prowl places a hold for the tier's worst case. The hold is not a
charge: at the end the run settles down to what it used and the rest is released. What
never happens is the reverse — you are not billed more than the hold, in any failure
mode.

If your balance cannot cover the hold for the tier that was picked, Prowl steps down —
`max` → `deep` → `basic` — to the highest tier you can actually afford, and tells you it
did. It does not refuse to run because the biggest tier does not fit.

## Report modules

A report is composed from a catalog of **33** intelligence
modules; the planner picks the ones the question needs. How many can appear in one
report depends on the tier: **8** on `basic`,
**12** on `deep`,
**16** on `max`.

## Cancelling

Cancel a subscription from the dashboard; it stays active until the end of the period
you paid for, then stops. Plan credit is a pool that ends with the plan — topped-up
credit survives it.

Deleting the account removes it and its data. That is not reversible, and it does not
refund a balance.

## Rate limits

Billing endpoints are limited to **5** requests per minute
per account. Everything else is in [rate limits](rate-limits.md).
