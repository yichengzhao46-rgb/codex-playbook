# Automatic Execution Route Audit

Use this workflow automatically for every non-trivial task after the PR validation profile has been inferred.

Its purpose is to make the ChatGPT / Codex / Mixed routing decision **automatic, inspectable, and traceable** without turning routine work into a logging exercise.

This workflow does not replace [`TASK_ROUTING.md`](../TASK_ROUTING.md) or [`task-routing-workflow.md`](task-routing-workflow.md). It records the decision and its outcome.

## Core rule

For every non-trivial task:

1. select the PR validation profile using `pr-auto-routing-workflow.md`;
2. select the execution route using `task-routing-workflow.md`;
3. create a compact **Route Receipt** before substantive execution;
4. update the receipt only if the route materially changes;
5. record the final execution outcome and validation evidence at completion.

Do not ask the user to choose ChatGPT, Codex, or Mixed when the task itself supplies enough information.

## What must be recorded

Use the compact fields in [`templates/route-receipt.md`](../templates/route-receipt.md):

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

The receipt is an audit record, not a second task plan. Keep it short.

## Persistence policy

### Chat-only or one-off reasoning tasks

Retain the Route Receipt in the active task context. Do not create a GitHub issue, file, or PR merely to store routing metadata.

If the user later asks which route or PR checks were used, surface the receipt directly.

### Repository changes with a branch or PR

Persist the final Route Receipt in one durable location, preferably:

1. the PR body;
2. a PR validation comment; or
3. an existing experiment / validation note.

Do not create a separate audit issue solely for the receipt.

### Workbench validation

For routing-rule validation, store the receipt and expected/observed route in the relevant `codex-workbench` experiment record.

## Reroute rule

A route change must be evidence-based, not preference-based.

Record a reroute only when one of these materially changes:

- authoritative object;
- dominant difficulty;
- required completion evidence;
- execution/verification burden;
- risk profile.

For every reroute, record:

```text
From:
To:
Trigger:
What changed:
New completion evidence:
```

Examples:

- `ChatGPT -> Mixed`: manuscript review reveals a raw-data recalculation required to resolve a quantitative claim.
- `ChatGPT -> Codex`: scientific wording is approved and the remaining work is a multi-file mechanical application.
- `Codex -> ChatGPT`: implementation reaches an unresolved scientific interpretation or policy conflict.

Do not record tool switching caused only by convenience, duplication, or a desire to involve both tools.

## Initial decision versus actual outcome

Distinguish the route selected before work from the route actually used.

A valid receipt can therefore show:

```text
Initial route: ChatGPT
Reroute history: ChatGPT -> Mixed because raw isotope recalculation became necessary
Final route: Mixed
```

This prevents retrospective rewriting of the routing decision and makes misroutes easier to identify.

## GitHub is not an executor route

Do not list `GitHub` as an alternative to ChatGPT or Codex.

GitHub is the durable state / provenance layer. Record its role separately as:

- `none`;
- `source of truth`;
- `commit`;
- `branch`;
- `PR`.

A GitHub operation may be initiated from ChatGPT or Codex, but the execution route remains ChatGPT, Codex, or Mixed.

## Silent by default, available on request

The audit should normally remain unobtrusive.

- Do not print a routing block before every ordinary answer.
- Surface the receipt when the route materially affects the user's workflow, when a handoff is required, when a PR is being created, or when the user asks for a routing audit.
- For Mixed work, include the route information in the task envelope or handoff so the receiving environment knows why it owns the next phase.

## Route-quality check at completion

At task completion, ask:

1. Did the selected route match the actual dominant difficulty?
2. Did another environment become necessary for a real verification reason?
3. Was there unnecessary ChatGPT <-> Codex ping-pong?
4. Was GitHub used only when durable state/review/provenance was useful?
5. Is the validation evidence tied to the final version actually checked?

If the route was materially wrong, record the mismatch as a validation finding rather than silently rewriting the receipt.

## Anti-patterns

Do not:

- create a GitHub log entry for every chat question;
- generate long route narratives;
- invent a `GitHub` execution route;
- treat PR class as proof of execution route;
- hide a reroute by replacing the initial decision;
- switch tools merely for symmetry;
- create repeated handoffs when one environment can finish;
- claim validation that was performed before a later material change.

## Positive validation cases

### Case 1 — Scientific manuscript review

Expected receipt:

```text
Primary PR profile: PR-RSCH
Secondary / specialist checks: PR-CAL, PR-AUTH as triggered
Initial route: ChatGPT
Dominant difficulty: scientific reasoning and evidence calibration
GitHub role: none
Final route: ChatGPT
```

### Case 2 — Approved multi-file mechanical edit

Expected receipt:

```text
Primary PR profile: PR-RSCH or relevant object class
Initial route: Codex
Dominant difficulty: repeated repository/file implementation and verification
Final route: Codex
```

### Case 3 — Scientific review escalates to deterministic recalculation

Expected receipt:

```text
Initial route: ChatGPT
Reroute history: ChatGPT -> Mixed because source-data recalculation became necessary
Final route: Mixed
```

## Negative controls

1. A direct factual explanation should not create a persistent routing artifact.
2. A DOCX manuscript scientific review should not route to Codex merely because the file format is Word.
3. A repository task should not route to Codex merely because GitHub is involved.
4. A task with several PR validation overlays should not become Mixed unless both reasoning and implementation are materially substantial.
5. A user asking to see the route audit should reveal the existing receipt rather than reconstructing a different route after the fact when the receipt is available.

## External benchmark adaptation

This workflow adopts two public design principles:

- route systems benefit from separating the initial routing decision from the observed execution outcome;
- a compact route receipt makes instruction-path compliance auditable.

Locally adapted behavior:

- no model-cost ranking;
- no mandatory database or state service;
- no GitHub artifact for chat-only tasks;
- no new executor category for GitHub;
- no additional handoff unless the existing task-routing policy already justifies one.

The goal is traceability with minimal ceremony.

## Completion criteria

The execution-route audit is functioning correctly when:

- every non-trivial task has an initial ChatGPT / Codex / Mixed route recorded;
- PR validation profile and execution route remain independent;
- required completion evidence and reroute threshold are recorded;
- reroutes preserve both the original decision and the reason for change;
- repository-backed work persists the receipt in an existing durable record;
- chat-only work does not create unnecessary GitHub logs;
- GitHub is recorded as provenance/state, not as a fourth executor;
- the user can ask what route was used and receive a compact, consistent answer;
- route-quality validation is tied to the final version actually completed.
