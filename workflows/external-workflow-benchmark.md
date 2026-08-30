# External Workflow Benchmark and Local Adaptation

Use this workflow before designing, materially restructuring, or promoting a reusable PR workflow, skill, routing rule, agent contract, validation gate, prompt framework, or operating method.

The purpose is to avoid reinventing established patterns while also preventing blind copying. External examples are design inputs only. The final method must be adapted to the user's actual working habits, prior successes, failure modes, repositories, and validation needs.

## Automatic trigger

Trigger this workflow automatically when a task asks to:

- design a new reusable PR class, workflow, skill, router, agent, template, or validation gate;
- materially update or restructure an existing reusable workflow or operating rule;
- convert an experimental method into a stable playbook method;
- solve a recurring workflow failure or inefficiency;
- decide among competing workflow architectures where public implementations may provide useful precedent.

Also trigger it when a proposed `PR-OPS` change introduces or materially changes reusable operating behavior.

Do not trigger it for:

- ordinary one-off execution of an already approved workflow;
- small wording, typo, formatting, or link-only documentation edits;
- routine repository maintenance whose method is already stable;
- tasks where the user explicitly asks not to use external sources.

## Stage 1 — Inspect local evidence first

Before searching externally, inspect the relevant local playbook and available validation history.

Identify:

- the current rule or workflow being changed;
- the user's stated objective;
- known successful patterns;
- known failure modes or misclassifications;
- existing PR classes, routing rules, templates, and validation gates that may overlap;
- whether the proposed change belongs in rules, prompts, workflows, templates, agents, or notes.

Do not search for an external pattern without first defining the local problem it is supposed to solve.

## Stage 2 — External benchmark search

Search current public sources, prioritizing:

1. official product or framework repositories and documentation;
2. mature open-source repositories with explicit agent/workflow instructions;
3. public examples of similar routing, handoff, review, validation, or skill systems;
4. evaluation-oriented repositories that expose test cases, negative controls, or review gates.

Prefer several complementary references over one repository when the design question is important.

Useful external objects include:

- `AGENTS.md` and repository instruction hierarchies;
- reusable skills or workflow directories;
- task-routing tables;
- planner/executor/reviewer separation;
- handoff schemas or task envelopes;
- validation freshness rules;
- risk overrides;
- review versus repair separation;
- positive and negative workflow evaluation cases.

## Stage 3 — Extract principles, not implementations

For each external pattern, classify it as:

- **Adopt** — directly useful and compatible with local practice;
- **Adapt** — useful principle but needs modification for the user's workflow;
- **Reject** — not suitable, too rigid, redundant, or inconsistent with local evidence;
- **Unresolved** — potentially useful but insufficiently tested.

Never copy a workflow merely because it is popular or well documented.

Record the design principle being borrowed, not just the repository name.

## Stage 4 — Local adaptation gate

Before adding an external idea to the playbook, answer:

1. Which concrete local problem does this solve?
2. Which past user experience, success, or failure supports the change?
3. What must be changed from the external version to fit the user's working style?
4. Does it duplicate or conflict with an existing rule?
5. Does it increase unnecessary handoffs, process overhead, or verification burden?
6. What failure mode could the adapted rule introduce?

Reject an external pattern when it adds ceremony without reducing a demonstrated risk or recurring burden.

User-specific operating experience has higher priority than external convention when the local evidence is stronger and the difference does not compromise correctness, safety, or reproducibility.

## Stage 5 — Design the adapted method

Build the smallest reusable change that solves the local problem.

Prefer:

- explicit trigger conditions;
- clear non-trigger conditions;
- one authoritative location for each stable rule;
- bounded handoffs;
- task-based rather than permission-based routing;
- proportionate validation;
- explicit evidence boundaries;
- compatibility with the existing PR taxonomy and task-routing workflow.

Avoid importing external terminology or architecture when the local system already has a clearer equivalent.

## Stage 6 — Validation before promotion

For meaningful new or changed workflow logic, define at least:

- one representative positive case that should trigger/use the method;
- one negative control that should not trigger/use it;
- an expected outcome or acceptance check;
- known untested edge cases.

Run forward validation in `codex-workbench` or another suitable execution repository when practical, especially for routing rules, mixed workflows, or behavior that is easy to over-apply.

A method may be promoted to stable only when the evidence supports the intended scope. Do not generalize one successful case to every possible scenario.

## Recommended design note

For significant changes, retain a compact benchmark note in the PR body or validation record:

```text
Local problem:
External patterns reviewed:
Adopt:
Adapt:
Reject:
User-experience evidence:
Local changes from external patterns:
Positive case:
Negative control:
Validation status:
Remaining boundary:
```

Do not turn stable playbook files into literature reviews. External-source detail belongs in the PR rationale, experiment record, or notes when useful; stable rules should remain concise and operational.

## Completion criteria

This benchmark is complete when:

- the local problem was defined before external searching;
- relevant public analogues were checked when available;
- adopted ideas are expressed as principles rather than copied text;
- each adopted/adapted idea is tied to a local need or user-experience signal;
- unsuitable external patterns are explicitly rejected when relevant;
- overlap with existing playbook rules was checked;
- trigger and non-trigger boundaries are explicit;
- meaningful new behavior has a positive case and negative control;
- promotion status is evidence-matched: experimental, validated, or stable.
