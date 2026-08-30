# Automatic PR Validation Router

Use this workflow automatically at the start of any non-trivial task that falls within the research, literature, data, figure, Origin, document, or Codex-operations domains covered by this playbook.

The user does **not** need to name a PR class. Infer the validation profile from the task itself.

`PR-*` labels in this repository serve two related purposes:

1. **task-level validation profile** — which checks should govern the work; and
2. **GitHub PR packaging class** — how a repository change should be described if a Pull Request is later created.

Selecting a task-level profile does not by itself require creating a GitHub Pull Request.

## Automatic entry rule

For every non-trivial in-scope task:

1. infer the authoritative object the user wants changed, checked, created, or validated;
2. assign one primary PR class;
3. load only the specialist checklist(s) materially relevant to the task;
4. choose ChatGPT, Codex, or Mixed execution independently using the task-routing workflow;
5. create a GitHub branch/PR only when the requested work or repository policy warrants it.

Do not ask the user to name `PR-RSCH`, `PR-DATA`, `PR-AUTH`, or another profile when the task description already provides enough information.

## Primary class auto-routing

| Task signal / authoritative object | Auto-selected primary profile |
| --- | --- |
| manuscript, thesis chapter, confirmation report, research argument, mechanism interpretation, claim-evidence review | `PR-RSCH` |
| literature search system, Zotero records/tags/attachments, evidence table, citation mapping | `PR-LIT` |
| spreadsheet analysis, quantitative calculation, statistics, calibration, qPCR/isotope/EEM processing, analysis script or derived table | `PR-DATA` |
| scientific figure source, visual semantics, layout, annotations, plot/schematic export | `PR-FIG` |
| editable Origin workbook/graph or `.opju` refinement | `PR-ORG` |
| DOCX/PDF structure, rendering, pagination, tracked changes, comments, native-document behavior | `PR-DOC` |
| reusable Codex skill, agent, router, prompt framework, MCP/plugin integration, automation, template, operating rule | `PR-OPS` |
| one genuinely atomic change spanning multiple authoritative objects that cannot be split without an invalid intermediate state | `PR-MIX` |

Route by the authoritative object, not merely by file extension. For example, a DOCX manuscript scientific argument is primarily `PR-RSCH`; use `PR-DOC` only for native document structure/render behavior or as a secondary checklist when needed.

## Specialist auto-triggers

Specialist workflows are overlays, not new top-level PR classes.

### `PR-AUTH` under `PR-RSCH`

Automatically load `workflows/pr-auth-academic-writing.md` when any of the following is material to the task:

- the user asks to check or reduce formulaic / AI-like academic writing;
- an AI-detector report or AI-writing concern is supplied;
- AI-assisted polishing or restructuring is being reviewed;
- academic voice, human authorship control, or evidence-preserving rewriting is a stated objective;
- a near-final manuscript/confirmation report is being comprehensively checked for scientific writing quality.

Do not load `PR-AUTH` for a narrow factual question or a purely quantitative recalculation with no prose-review component.

### Data escalation from research writing

A `PR-RSCH` review should automatically add `PR-DATA` validation when a suspected conflict cannot be resolved from the manuscript alone and requires deterministic recalculation, raw-data verification, formula reconstruction, unit conversion, or statistical checking.

Do not call a numerical mismatch a confirmed conflict before same-basis / same-definition checks are completed.

### Document overlay

Add a `PR-DOC` secondary checklist when a manuscript task also requires native DOCX/PDF review such as tracked changes, comments, pagination, heading structure, figure/table placement, rendering, or cross-reference integrity.

A DOCX file by itself does not make the task primarily `PR-DOC`.

### Figure and Origin overlay

- A figure embedded in a manuscript is primarily `PR-FIG` when the figure source, data mapping, visual semantics, annotation, or export is changed.
- Add `PR-DOC` only for placement/rendering in the document.
- Use `PR-ORG` when the authoritative editable deliverable is an Origin workbook/graph or `.opju` project.
- Add `PR-DATA` when calculation or statistical logic also changes.

### Skill lifecycle under `PR-OPS`

Automatically route skill creation or material skill updates to the repository's approved skill-lifecycle checklist when that workflow is present in the current approved playbook.

Trigger examples:

- create a reusable Codex skill;
- materially change a skill trigger description;
- restructure SKILL.md or its references/scripts/assets;
- promote an experimental skill into stable use.

Ordinary use of an already-approved skill does not become `PR-OPS`; classify the actual task artifact instead.

### External agent / integration under `PR-OPS`

Automatically route evaluation, installation, configuration, or promotion of a third-party agent/tool integration to the approved external-agent integration checklist when present.

Trigger examples:

- Agent Reach or similar external-source agents;
- new MCP/plugin/tool integrations;
- integrations that install dependencies, access external services, use credentials, execute shell/package-manager commands, or alter persistent local configuration.

Prefer already-connected or built-in tools when they satisfy the task. Do not install an external integration merely because one exists.

## Primary versus secondary profile rules

1. Choose exactly one primary class unless `PR-MIX` is justified.
2. Add secondary checklists only for actual cross-boundary validation needs.
3. Consulting another artifact does not automatically add its PR class.
4. File format is weaker than task intent and authoritative object.
5. Project key is a routing hint, never the primary-class authority.
6. Do not use `PR-MIX` as a shorthand for "several checks are involved."

## `PR-MIX` anti-abuse gate

Use `PR-MIX` only when all are true:

- at least two authoritative objects are changed;
- the objects belong to different PR classes;
- they share one atomic change boundary;
- splitting creates an invalid or unusable intermediate state;
- the union of all constituent validation gates can be applied;
- the reason not to split is documented.

If independent changes merely happen in the same task, keep separate primary work units or PRs.

## Execution route is independent

After selecting the validation profile, separately choose the execution environment using `workflows/task-routing-workflow.md`:

- reasoning / interpretation / writing dominated → usually ChatGPT;
- repository implementation / repeated execution / tests dominated → usually Codex;
- both substantial → Mixed.

Examples:

- "Check my confirmation-report DOCX for scientific logic and AI-like writing" → `PR-RSCH` + `PR-AUTH` + optional `PR-DOC`; ChatGPT-led or Mixed depending on document-processing needs.
- "Recalculate isotope excess from raw Excel and update analysis code" → `PR-DATA`; Codex-heavy or Mixed.
- "Create a reusable skill for Zotero tag cleanup" → `PR-OPS` skill lifecycle; Codex-heavy implementation with review.
- "Fix only page breaks and caption placement in a completed DOCX" → `PR-DOC`.

## Silent routing by default

Do not burden the user with internal routing details on routine tasks.

- Apply the correct profile automatically.
- Mention the selected route only when it materially affects scope, risk, validation, handoff, or the user's requested workflow.
- If ambiguity would change the scientific conclusion, destructive action, or required validation, clarify the substantive ambiguity rather than asking the user to choose a PR label.

## Re-routing during execution

Re-route when the authoritative object or required evidence materially changes.

Examples:

- manuscript review reveals a quantitative issue needing recalculation → retain `PR-RSCH`, add `PR-DATA` validation for that finding;
- data analysis expands into redesigning figure semantics → primary work may split into `PR-DATA` and `PR-FIG`, or become `PR-MIX` only if atomicity is proven;
- one-off workflow fix becomes a reusable Codex rule → route that reusable-method change separately as `PR-OPS`.

Do not keep stale routing merely because the task started under a different profile.

## Minimum internal routing record

For non-trivial work, retain internally or in the PR/task record:

```text
Authoritative object:
Primary PR profile:
Secondary/specialist checklists:
Execution route: ChatGPT | Codex | Mixed
Required evidence:
Escalation condition:
GitHub PR needed: yes | no | later
```

The user should not have to supply these fields.

## Positive validation cases

1. **Near-final research DOCX review**
   - Input: manuscript/confirmation report with data, argument, and prose.
   - Expected: `PR-RSCH`; auto-add `PR-AUTH` for comprehensive writing/authorship review; add `PR-DOC` only if native document QA is requested/material.

2. **Raw quantitative analysis**
   - Input: spreadsheet + request to calculate, statistically test, or regenerate derived data.
   - Expected: `PR-DATA`, regardless of whether results will later enter a manuscript.

3. **Reusable Codex skill creation**
   - Input: request to create/update a reusable skill.
   - Expected: `PR-OPS` + skill-lifecycle specialist workflow when approved.

4. **Third-party agent integration**
   - Input: request to install/evaluate Agent Reach or a similar integration.
   - Expected: `PR-OPS` + external-agent integration specialist workflow when approved.

## Negative controls

1. A user asks what a scientific term means → no PR validation profile needs to be surfaced; answer directly.
2. A manuscript contains a figure but only prose is revised → `PR-RSCH`, not automatically `PR-FIG`.
3. A DOCX is uploaded for scientific argument review → do not classify primarily as `PR-DOC` solely because of file type.
4. An approved skill is used to perform a data task → classify the task as `PR-DATA`, not `PR-OPS`.
5. A data fix and an unrelated figure-color preference occur together → split; do not use `PR-MIX`.

## Completion criteria

The auto-router is functioning correctly when:

- users can describe the task normally without naming PR classes;
- one primary validation profile is inferred from the authoritative object;
- specialist checklists are loaded only when their trigger conditions are met;
- ChatGPT/Codex/Mixed routing remains independent from PR classification;
- GitHub Pull Requests are created only when warranted, not merely because a PR validation profile was selected;
- `PR-MIX` remains restricted to atomic cross-class changes;
- re-routing occurs when the required evidence materially changes;
- routine routing remains mostly invisible to the user.
