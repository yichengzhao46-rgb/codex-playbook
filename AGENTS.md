# AGENTS.md — Codex Playbook

## Mission

This repository is the canonical methods library for how Codex should be instructed, governed, reviewed, and improved.

## Scope

Store reusable Codex methods here, including:
- prompts and prompt patterns
- agent operating rules
- pull request and review workflows
- MCP and tool-use practices
- task templates
- reusable checklists
- lessons learned and validated examples

Do not store project-specific raw data, manuscript datasets, generated scientific results, or unrelated production code here.

## Default working rules

1. Inspect existing repository context before editing.
2. For every non-trivial in-scope task, automatically apply [`workflows/pr-auto-routing-workflow.md`](workflows/pr-auto-routing-workflow.md) before execution. Infer the primary PR validation profile and any specialist checklist from the task itself; do not require the user to name a PR class.
3. For `PR-RSCH` tasks that evaluate, rewrite, strengthen, weaken, or adjudicate scientific claims or mechanism interpretations, automatically apply [`workflows/pr-cal-evidence-calibration.md`](workflows/pr-cal-evidence-calibration.md). Evaluate both overclaim and underclaim risk and prefer the strongest defensible claim rather than the most cautious possible wording.
4. Select ChatGPT, Codex, or Mixed execution independently from the PR validation profile using the task-routing policy. For every non-trivial task, automatically create and maintain the lightweight [`workflows/execution-route-audit.md`](workflows/execution-route-audit.md) Route Receipt so the initial route, reroutes, final route, and completion evidence are traceable. Do not create GitHub state solely to log a chat-only task.
5. For non-trivial changes, make a short implementation plan before modifying files.
6. Keep each change focused on one logical objective.
7. Prefer a dedicated branch for meaningful changes.
8. Prefer Draft Pull Requests for Codex-generated work.
9. Do not merge meaningful changes automatically unless explicitly instructed.
10. Review the final diff before proposing completion.
11. Preserve existing working behavior unless the task explicitly requires breaking changes.
12. Do not invent tool capabilities, files, test results, or external state.
13. Distinguish clearly between validated practice, experimental practice, and speculation.
14. Before designing or materially restructuring a reusable PR workflow, skill, router, agent, validation gate, prompt framework, or operating method, apply the [External Workflow Benchmark and Local Adaptation](workflows/external-workflow-benchmark.md) workflow unless the task falls under its explicit non-trigger conditions.
15. When `WF-RNA-DUAL` is invoked, apply both [`workflows/bath-rp-species-resolved-transcriptomics.md`](workflows/bath-rp-species-resolved-transcriptomics.md) and its mandatory companion [`workflows/wf-rna-dual-figure-gating.md`](workflows/wf-rna-dual-figure-gating.md). Stage gating controls analysis progression; figure gating controls publication-figure progression within each stage. If the current stage contains an unfinished required figure, `continue WF-RNA-DUAL` advances only to the next figure checkpoint, not to the next stage.

## Documentation rules

- Write reusable guidance, not conversation-specific notes.
- Prefer concise operational instructions over long narrative explanations.
- Add examples when they materially improve reproducibility.
- Keep stable policies in `rules/` and task-ready instructions in `prompts/`.
- Put end-to-end procedures in `workflows/`.
- Put copy-ready task skeletons in `templates/`.

## Pull request standard

Every meaningful PR should state:
- what changed
- why it changed
- files or areas affected
- validation or tests performed
- known limitations
- whether the change is stable or experimental

For reusable operating-method changes that trigger external benchmarking, the PR should also summarize the external patterns reviewed, what was adopted/adapted/rejected, the local user-experience signal that justified the change, and the validation boundary.

For repository-backed non-trivial work, preserve the final Route Receipt in the PR body/comment or an existing validation record when practical. The receipt should remain compact and must not become a duplicate task narrative.

## Safety and reversibility

- Never overwrite or remove important material without a clear reason.
- Prefer additive, reviewable changes.
- Keep changes easy to revert.
- Avoid committing secrets, tokens, credentials, or private keys.

## Continuous improvement

When a Codex workflow succeeds repeatedly, promote it into a reusable method.
When a workflow fails, record the failure mode and corrected pattern in `notes/` or update the relevant rule.
External conventions are inputs, not authority: adapt them to demonstrated local needs and reject patterns that add ceremony without reducing a real failure mode or recurring burden.
