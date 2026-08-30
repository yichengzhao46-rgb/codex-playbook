# Task Routing Workflow

Use this workflow to decide whether a task should be executed in ChatGPT, Codex, or a mixed workflow.

This file is the operational companion to [`TASK_ROUTING.md`](../TASK_ROUTING.md). The policy explains the routing principles; this workflow provides the minimum intake and execution procedure.

## Entry condition

Use this workflow when the correct execution environment is not obvious, when a task spans reasoning and implementation, or when the route may change as the task evolves.

Do not invoke a multi-tool workflow merely because both tools are available. Direct execution remains the default when one environment can complete and verify the task adequately.

## Procedure

1. **State the objective.**
   - Define the actual deliverable rather than the current application, repository, or conversation context.

2. **Identify the dominant difficulty.**
   - Reasoning, interpretation, synthesis, writing, or decision-making → ChatGPT-leaning.
   - Repository implementation, deterministic execution, repeated file operations, tests, builds, debugging, or edit-run-debug loops → Codex-leaning.
   - Both are substantial → Mixed.

3. **Define completion evidence.**
   - Ask what evidence is required to call the task complete.
   - Examples: evidence-backed scientific judgment, approved wording, passing tests, deterministic recalculation, no stale references, validated export, or reviewed diff.

4. **Classify the task.**
   - Use the closest task class from `TASK_ROUTING.md`, such as research/review, documentation, diagnosis, implementation, verification, or mixed.

5. **Select the route.**
   - `ChatGPT`: reasoning/interpretation/writing dominates and executable validation is not material.
   - `Codex`: implementation/execution/verification dominates and the decision boundary is already clear.
   - `Mixed`: a non-trivial reasoning phase must define the work before executable implementation or verification.

6. **Select the PR class independently when packaging a repository change.**
   - Apply the research PR routing rules if the work becomes a reviewable repository change.
   - Do not infer execution route from PR class, project key, repository name, or assumed tool permissions.

7. **If Mixed, create a task envelope.**
   - Use [`templates/task-envelope.md`](../templates/task-envelope.md).
   - Prefer one deliberate handoff rather than repeated ChatGPT ↔ Codex bouncing.
   - Keep one primary writer for an active change set.

8. **Define escalation conditions before execution.**
   - State what change in task nature would require re-routing.
   - Examples: raw-data recalculation becomes necessary; approved wording expands into a multi-file mechanical migration; a runtime defect requires repeated execution; a coding task reaches an unresolved scientific interpretation.

9. **Execute and verify in the selected environment.**
   - Match verification to the task's actual failure modes.
   - Keep failed, blocked, and unrun checks explicit.

10. **Re-route only when the task materially changes.**
    - Do not switch tools for symmetry, preference, or duplication.
    - Re-route when the dominant difficulty, required evidence, or risk profile changes.

## Compact routing output

```text
Route: ChatGPT | Codex | Mixed
Task class:
Reason:
ChatGPT role:
Codex role:
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
- required completion evidence is stated;
- ChatGPT, Codex, or Mixed is selected for a task-based reason;
- PR class, if needed, is selected independently from the execution route;
- escalation conditions are stated for non-trivial work;
- Mixed work has a bounded task envelope and one primary writer;
- the selected validation addresses the likely failure mode rather than merely confirming that files changed.

## Forward-validation status

The core routing policy has been forward-validated in `codex-workbench` using:

- a scientific evidence-synthesis / manuscript-review task that correctly routed to ChatGPT;
- a related raw-isotope recalculation and plotting-script task that escalated to Mixed/Codex-heavy execution; and
- an approved scientific wording change applied mechanically across many files that correctly routed to Codex.

This validates the core separation between **what is being changed** and **where the difficult part should be executed**. Broader edge cases should continue to be recorded and used to refine the policy.
