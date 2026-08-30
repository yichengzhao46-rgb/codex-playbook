# Task Routing Workflow

Use this workflow to decide whether a task should be executed in ChatGPT, Codex, or a mixed workflow.

This file is the operational companion to [`TASK_ROUTING.md`](../TASK_ROUTING.md). The policy explains the routing principles; this workflow provides the minimum intake and execution procedure.

## Relationship to PR validation routing

Execution routing and PR validation routing are independent decisions.

For every non-trivial in-scope task, first or in parallel apply [`pr-auto-routing-workflow.md`](pr-auto-routing-workflow.md) to infer the primary `PR-*` validation profile and any specialist checklist. The user does not need to name a PR class.

Then use this workflow to choose **where** the difficult part should be executed: ChatGPT, Codex, or Mixed.

A task-level `PR-*` profile does not by itself require a GitHub Pull Request. A GitHub PR is created only when the task or repository workflow warrants a reviewable repository change.

## Entry condition

Use this workflow when the correct execution environment is not obvious, when a task spans reasoning and implementation, or when the route may change as the task evolves.

Do not invoke a multi-tool workflow merely because both tools are available. Direct execution remains the default when one environment can complete and verify the task adequately.

## Procedure

1. **State the objective.**
   - Define the actual deliverable rather than the current application, repository, or conversation context.

2. **Apply the automatic PR validation profile.**
   - Infer the authoritative object and primary PR class using `pr-auto-routing-workflow.md`.
   - Load only specialist overlays materially required by the task.
   - Do not ask the user to choose a PR label when the task description is sufficient.

3. **Identify the dominant difficulty.**
   - Reasoning, interpretation, synthesis, writing, or decision-making → ChatGPT-leaning.
   - Repository implementation, deterministic execution, repeated file operations, tests, builds, debugging, or edit-run-debug loops → Codex-leaning.
   - Both are substantial → Mixed.

4. **Define completion evidence.**
   - Ask what evidence is required to call the task complete.
   - Examples: evidence-backed scientific judgment, approved wording, passing tests, deterministic recalculation, no stale references, validated export, or reviewed diff.

5. **Classify the task.**
   - Use the closest task class from `TASK_ROUTING.md`, such as research/review, documentation, diagnosis, implementation, verification, or mixed.

6. **Select the route.**
   - `ChatGPT`: reasoning/interpretation/writing dominates and executable validation is not material.
   - `Codex`: implementation/execution/verification dominates and the decision boundary is already clear.
   - `Mixed`: a non-trivial reasoning phase must define the work before executable implementation or verification.

7. **Decide GitHub packaging independently.**
   - If the work becomes a reviewable repository change, use the already-selected PR class for packaging.
   - Do not create a GitHub PR merely because a task-level PR validation profile was applied.
   - Do not infer execution route from PR class, project key, repository name, or assumed tool permissions.

8. **If Mixed, create a task envelope.**
   - Use [`templates/task-envelope.md`](../templates/task-envelope.md).
   - Prefer one deliberate handoff rather than repeated ChatGPT ↔ Codex bouncing.
   - Keep one primary writer for an active change set.

9. **Define escalation conditions before execution.**
   - State what change in task nature would require re-routing.
   - Examples: raw-data recalculation becomes necessary; approved wording expands into a multi-file mechanical migration; a runtime defect requires repeated execution; a coding task reaches an unresolved scientific interpretation.

10. **Execute and verify in the selected environment.**
    - Match verification to the task's actual failure modes and the selected PR validation profile.
    - Keep failed, blocked, and unrun checks explicit.

11. **Re-route only when the task materially changes.**
    - Do not switch tools for symmetry, preference, or duplication.
    - Re-route when the authoritative object, dominant difficulty, required evidence, or risk profile changes.

## Compact routing output

Retain internally or surface only when useful:

```text
Authoritative object:
Primary PR profile:
Secondary/specialist checklist:
Route: ChatGPT | Codex | Mixed
Task class:
Reason:
GitHub output: none | commit | branch | PR
Acceptance check:
Escalate if:
```

## Review and repair rule

For review findings, keep these stages separate:

`finding → verification → accept/reject → repair → re-verification`

A reviewer comment is not automatically an instruction to edit. For scientific, statistical, runtime, or factual findings, verify the finding before repair when possible.

## Validation freshness

Validation is tied to the version actually checked.

- Meaningful tracked code or test changes invalidate affected executable verification.
- Meaningful scientific interpretation changes invalidate affected claim-level review.
- Re-run the relevant check after accepted repairs.
- Documentation-only work should use proportionate review rather than artificial code gates.

## Completion criteria

The routing step is complete when:

- the objective and dominant difficulty are explicit;
- the authoritative object and primary PR validation profile have been inferred automatically for non-trivial in-scope work;
- specialist overlays are loaded only when triggered;
- required completion evidence is stated;
- ChatGPT, Codex, or Mixed is selected for a task-based reason;
- GitHub PR creation is decided independently from validation-profile selection;
- escalation conditions are stated for non-trivial work;
- Mixed work has a bounded task envelope and one primary writer;
- the selected validation addresses the likely failure mode rather than merely confirming that files changed.

## Forward-validation status

The core execution-routing policy has been forward-validated in `codex-workbench` using:

- a scientific evidence-synthesis / manuscript-review task that correctly routed to ChatGPT;
- a related raw-isotope recalculation and plotting-script task that escalated to Mixed/Codex-heavy execution; and
- an approved scientific wording change applied mechanically across many files that correctly routed to Codex.

The new automatic PR validation router requires its own forward validation before stable promotion. At minimum validate one representative research-writing case, one quantitative case, one reusable-skill case, and the negative controls defined in `pr-auto-routing-workflow.md`.
