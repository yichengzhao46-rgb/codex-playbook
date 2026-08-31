# Codex Playbook

A personal methods library for using Codex consistently, safely, and reproducibly across software, research, automation, and agent workflows.

## Purpose

This repository defines **how Codex should work**. It stores reusable instructions, prompts, operating rules, review patterns, workflow templates, MCP practices, skills, and lessons learned. It is not intended to hold project-specific experimental data or production outputs.

## Relationship to codex-workbench

- **codex-playbook** = methods, rules, prompts, templates, skills, and standards.
- **codex-workbench** = execution, experiments, prototypes, integrations, and validation.

Methods should be developed and refined here, then applied and tested in `codex-workbench` or other project repositories.

## Task routing

See [`TASK_ROUTING.md`](TASK_ROUTING.md) for the current policy on when to use ChatGPT, when to use Codex, and when a mixed workflow is more efficient. Routing is based on task nature, verification needs, and total execution cost rather than a fixed permission boundary.

For operational use:

- [`workflows/task-routing-workflow.md`](workflows/task-routing-workflow.md) — minimum intake and execution procedure for choosing ChatGPT, Codex, or Mixed.
- [`workflows/execution-route-audit.md`](workflows/execution-route-audit.md) — automatic lightweight Route Receipt for recording the initial route, evidence-based reroutes, final route, and completion evidence.
- [`templates/route-receipt.md`](templates/route-receipt.md) — compact auditable routing record; chat-only tasks stay in task context rather than creating unnecessary GitHub logs.
- [`templates/task-envelope.md`](templates/task-envelope.md) — bounded handoff template for Mixed workflows.

## Research analysis skills

- [`skills/literature-guided-analysis/SKILL.md`](skills/literature-guided-analysis/SKILL.md) — **stable / forward-validated once** recommendation-first workflow that uses published literature to interpret user data patterns, generate 3–5 candidate analysis directions, distinguish current-data analysis from new evidence generation, and produce a detailed plan after user selection.

## Workspace maintenance skills

- [`skills/project-artifact-cleanup/SKILL.md`](skills/project-artifact-cleanup/SKILL.md) — **experimental** reversible cleanup workflow for classifying project files as KEEP / SAFE-DELETE / ARCHIVE / REVIEW, isolating preview/render/temp artifacts, protecting research sources and Git-tracked work, and requiring a dry-run plus second deletion manifest before permanent removal.

## Repository structure

```text
codex-playbook/
├── AGENTS.md
├── TASK_ROUTING.md
├── prompts/
├── workflows/
├── rules/
├── templates/
├── skills/
├── mcp/
├── agents/
├── examples/
└── notes/
```

## Core operating principles

1. Prefer explicit, reusable instructions over ad hoc prompting.
2. Keep stable rules separate from task-specific prompts.
3. Use task-specific branches for non-trivial changes.
4. Prefer Draft Pull Requests for Codex-generated changes.
5. Require review before merge for meaningful changes.
6. Preserve provenance, reproducibility, and reversibility.
7. Record successful patterns and failed approaches so the playbook improves over time.

## Change workflow

For meaningful updates to this repository:

`Issue or task → plan → branch → edit → self-check → Draft PR → review → merge`

The default branch should represent the current approved operating system for Codex usage.
