# Playbooks

By default `prowl_analyze` composes the report for the question: the planner picks which
of the **33** intelligence modules the request actually
needs, so two different questions produce two differently-shaped reports.

A playbook overrides that. It forces a fixed, persona-tuned shape — the same sections, in
the same order, every time.

```json
{
  "tool": "prowl_analyze",
  "query": "example.com",
  "playbook_id": "<id from prowl_list_playbooks>",
  "execution_mode": "deep"
}
```

`prowl_list_playbooks` returns the ones available to your account, with what each is for.

## When a fixed shape is the right choice

- **Comparing runs over time.** A report that changes shape between runs cannot be
  diffed. A playbook makes month two comparable to month one.
- **Handing the output to someone else.** A stakeholder who learns where to look should
  find the same thing there next time.
- **Feeding a downstream system.** Anything parsing the report needs a stable contract,
  and "the planner chose well today" is not one.

## When to let the planner choose

- **You do not know what the question needs yet.** That is what the planner is for.
- **The question is unusual.** A playbook built for a competitor sweep will answer a
  competitor sweep, whatever you asked.
- **You want the widest coverage the tier allows.** A fixed shape spends its budget on
  its own sections, including the ones your question did not need.

## What a playbook does not change

The tier still sets the ceiling, the verification pass still runs, and the report still
opens with the market it resolved and closes with what it could not confirm. A playbook
chooses the shape of the answer, not the standard of evidence behind it.
