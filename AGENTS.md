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
2. For non-trivial changes, make a short implementation plan before modifying files.
3. Keep each change focused on one logical objective.
4. Prefer a dedicated branch for meaningful changes.
5. Prefer Draft Pull Requests for Codex-generated work.
6. Do not merge meaningful changes automatically unless explicitly instructed.
7. Review the final diff before proposing completion.
8. Preserve existing working behavior unless the task explicitly requires breaking changes.
9. Do not invent tool capabilities, files, test results, or external state.
10. Distinguish clearly between validated practice, experimental practice, and speculation.
11. Before designing or materially restructuring a reusable PR workflow, skill, router, agent, validation gate, prompt framework, or operating method, apply the [External Workflow Benchmark and Local Adaptation](workflows/external-workflow-benchmark.md) workflow unless the task falls under its explicit non-trigger conditions.
12. For every substantive academic-prose revision, automatically apply [PR-AUTH](workflows/pr-auth-academic-writing.md), including academic-style review, qualitative AI-writing-risk review, and meaning-diff validation.
13. For document/file edits, never overwrite the only recoverable original. Prefer an untouched original plus a versioned revised copy; otherwise use a dedicated version-controlled branch or verify a backup before in-place overwrite.

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

For substantive academic-prose changes, the PR or task completion record should also state:
- whether PR-AUTH was run;
- the qualitative AI-writing-risk result for changed text;
- whether the original was preserved;
- where the revised copy/branch lives and how to roll back.

## Safety and reversibility

- Never overwrite or remove important material without a clear reason.
- Prefer additive, reviewable changes.
- Keep changes easy to revert.
- For manuscripts and other important documents, preserve the original by default and create a clearly versioned revised output.
- Avoid committing secrets, tokens, credentials, or private keys.

## Continuous improvement

When a Codex workflow succeeds repeatedly, promote it into a reusable method.
When a workflow fails, record the failure mode and corrected pattern in `notes/` or update the relevant rule.
External conventions are inputs, not authority: adapt them to demonstrated local needs and reject patterns that add ceremony without reducing a real failure mode or recurring burden.
