# Your first report

`prowl_analyze` is not a search. It plans a graph of tool calls, runs them, checks the
resulting claims against independent tools, then writes a structured report from what
survived.

```json
{
  "tool": "prowl_analyze",
  "query": "competitive landscape for example.com in the US",
  "execution_mode": "basic"
}
```

## What happens, in order

1. **Classify.** Some requests are a conversation, not a research job; those end here
   with an answer and no report.
2. **Plan.** A dependency graph of tool calls, budgeted for the tier.
3. **Execute.** The graph runs. Most of it is plain Python calling providers.
4. **Verify.** Claims are extracted and cross-checked; numeric ones are re-derived from a
   second, independent tool where one exists. Refuted claims are kept, not dropped.
5. **Compose.** The report's sections are chosen for the question, then written in
   parallel — each against the verified claims for its area.

## Tiers

| Tier | Provider-cost ceiling | Modules in one report |
|---|---|---|
| `basic` | $2.5 | up to 8 |
| `deep` | $8 | up to 12 |
| `max` | $18 | up to 16 |

The ceiling is a ceiling, not a price — see [billing](../billing.md).

## Blocking or async

A blocking call returns the report and holds the connection for the whole run. That is
fine from a script and often wrong from an IDE client, which may time out before Prowl
finishes.

The async shape does not care:

```json
{ "tool": "prowl_start_session", "query": "…", "execution_mode": "deep" }
```

then poll `prowl_session_status` with the returned id, and fetch the result with
`prowl_get_session`. The run proceeds whether or not anything is watching.

## The first line of every report

A report opens by naming the market it resolved — country and language — and **how** it
resolved it: stated by you, inferred from your request, or assumed because nobody said.
One run is one market; it cannot straddle two.

If the market matters, say it in the query. Inference is deliberately conservative — full
country names, demonyms and country domains only — because a wrong inference is worse
than a stated assumption, which announces itself.

## Follow-up questions

Pass the same `session_id` on the next call and the conversation, the report cache and
the circuit-breaker state all carry over. Asking about a report you already ran does not
re-run it.

## Reading the result

Three parts people skip and shouldn't:

- **The coverage line.** What the run could not cover, stated plainly.
- **Contradictions.** Where two independent tools disagreed, both numbers with their
  sources.
- **The refuted appendix.** Claims that failed verification, kept so you can see what was
  considered and rejected.

An agent that reports only what it confirmed is easy to build. The appendix is the part
that makes the rest worth trusting.
