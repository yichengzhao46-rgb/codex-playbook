# Codex Playbook

A personal methods library for using Codex consistently, safely, and reproducibly across software, research, automation, and agent workflows.

## Purpose

This repository defines **how Codex should work**. It stores reusable instructions, prompts, operating rules, review patterns, workflow templates, MCP practices, and lessons learned. It is not intended to hold project-specific experimental data or production outputs.

## Relationship to codex-workbench

- **codex-playbook** = methods, rules, prompts, templates, and standards.
- **codex-workbench** = execution, experiments, prototypes, integrations, and validation.

Methods should be developed and refined here, then applied and tested in `codex-workbench` or other project repositories.

## Repository structure

```text
codex-playbook/
├── AGENTS.md
├── prompts/
├── workflows/
├── rules/
├── templates/
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
