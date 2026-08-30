# Task Envelope Template

Use this template for a deliberate ChatGPT → Codex or Codex → ChatGPT handoff when a Mixed route is justified.

Remove fields that are genuinely irrelevant, but keep the handoff bounded and evidence-aware.

```text
Objective:

Acceptance criteria:

Scope:

Non-goals:

Relevant evidence / decisions:

Constraints / allowed actions:

Primary writer:

Required output:

Validation required:

GitHub target, if any:

Escalate if:
```

## Handoff rules

- Transfer the decision state, not the entire conversation history.
- Include only evidence and constraints needed to execute the next phase correctly.
- Do not invent files, formulas, implementation details, or validation results that the receiving environment can inspect directly.
- Keep one primary writer for an active change set.
- Reviewer/tester roles should remain read-only until a finding is accepted for repair.
- If the task's dominant difficulty changes, re-run the task-routing workflow instead of extending the envelope indefinitely.

## Example

```text
Objective:
Recalculate background-corrected absolute 13C excess from the authoritative raw workbook and update the plotting script.

Acceptance criteria:
- use the approved isotope definitions and background correction;
- preserve biological replicate structure;
- verify units and formulas deterministically;
- regenerate the summary table;
- update the plot without changing scientific interpretation.

Scope:
Raw isotope workbook, calculation script, summary output, paired plot source.

Non-goals:
Do not strengthen species-specific carbon-fixation claims or rewrite the manuscript interpretation.

Relevant evidence / decisions:
Bulk EA-IRMS is community-level; delta13C, atom% 13C, and absolute 13C excess are distinct reporting layers; the approved background definition must be preserved.

Constraints / allowed actions:
Inspect source files before editing; keep raw inputs unchanged; document formulas; report unresolved assumptions rather than silently filling gaps.

Primary writer:
Codex.

Required output:
Reproducible calculations, updated script/output, validation summary, and reviewable diff if repository files change.

Validation required:
Independent formula/unit check, representative-row recalculation, output consistency check, and rerun after any accepted code fix.

GitHub target, if any:
Task branch / Draft PR.

Escalate if:
The source data cannot resolve the background definition, the calculation requires a new scientific assumption, or the requested figure wording would change claim strength.
```
