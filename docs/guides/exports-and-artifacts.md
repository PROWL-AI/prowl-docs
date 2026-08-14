# Exports & artifacts

A report is text and structure. An artifact is that report rendered into something you
can send someone: **infographic, pdf, pptx, video, audio** — 5 types.

## They do not come for free with a report

This is the single most common wrong expectation, so it is stated plainly:
`prowl_analyze` produces **no artifact**. Artifacts are generated on demand, by a
separate call, and billed separately.

```json
{
  "tool": "prowl_generate_artifact",
  "session_id": "<the session that ran the report>",
  "artifact_type": "pdf"
}
```

That is deliberate. Rendering a deck and a video costs real time and real money, and
most runs want neither — paying for five renders on every analysis would make the cheap
tier expensive for everyone who only wanted the numbers.

## The session is the link

Both `prowl_generate_artifact` and `prowl_export_report` work on a **cached report**, so
they need the `session_id` of a prior `prowl_analyze` on the same session. Without one
there is nothing to render, and the call fails rather than silently running a new
analysis.

Pass a stable `session_id` across consecutive calls and the report cache, the
conversation history and the circuit-breaker state all stay scoped to one conversation.

## Which one to use

| | |
|---|---|
| `prowl_generate_artifact` | produce one artifact of a given type from the cached report |
| `prowl_export_report` | export the cached report in another format |

Generate an artifact when you want a rendered object. Export when you want the same
content in a different file format.

## Practical notes

- **Render time varies by type.** Text-shaped formats return quickly; video is the slow
  one by a wide margin.
- **Generate what you will actually send.** Each type is a separate charge, and five
  artifacts of one report cost five renders.
- **Re-generating is a new render.** The report is cached; the artifact is not.
