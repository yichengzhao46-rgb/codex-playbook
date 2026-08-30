# Route Receipt Template

Use this compact record for non-trivial ChatGPT / Codex / Mixed routing decisions.

Keep it short. It is an audit receipt, not a second task plan.

```text
Authoritative object:
Primary PR profile:
Secondary / specialist checks:
Initial route: ChatGPT | Codex | Mixed
Dominant difficulty:
Required completion evidence:
Primary executor / writer:
GitHub role: none | source of truth | commit | branch | PR
Escalate / reroute if:
Reroute history: none | <from -> to + reason>
Final route:
Validation performed:
Persistent record location: chat | task note | commit | PR body/comment | validation record
```

## Reroute entry

When a material reroute occurs, append rather than overwrite:

```text
From:
To:
Trigger:
What changed:
New completion evidence:
```

## Persistence rule

- Chat-only task: retain in active task context; do not create GitHub state solely for routing metadata.
- Branch/PR task: persist the final receipt in the PR body, a PR validation comment, or an existing validation record.
- Mixed handoff: include the relevant receipt fields in the task envelope.
- Workbench validation: record expected versus observed route and reroutes in the experiment record.

## Visibility rule

Do not surface this block automatically for every ordinary task. Show it when:

- the user asks which route was used;
- a handoff is required;
- a route change materially affects workflow;
- a PR/validation record is being created;
- routing itself is under validation.
