# PR-OPS Specialist Routing

Use this rule after a change has already been classified as `PR-OPS` and the authoritative object is a reusable Codex skill, agent/tool integration, or related operating method.

This rule does not add new top-level PR classes. It selects a specialist checklist within `PR-OPS`.

## Routing table

| Changed object or task | Primary PR class | Specialist workflow | Secondary checklist |
| --- | --- | --- | --- |
| create or update a Codex skill | `PR-OPS` | [`../workflows/skill-lifecycle-workflow.md`](../workflows/skill-lifecycle-workflow.md) | domain class only if another authoritative object also changes |
| change skill trigger/description/router | `PR-OPS` | skill lifecycle + routing validation | add positive/negative trigger cases |
| promote an experimental skill to stable | `PR-OPS` | skill lifecycle | require forward-validation evidence |
| install/evaluate Agent Reach or another third-party agent integration | `PR-OPS` | [`../workflows/external-agent-integration-workflow.md`](../workflows/external-agent-integration-workflow.md) | security/credential boundary within the same workflow |
| add one new Agent Reach channel | `PR-OPS` | external-agent integration | validate only the added channel unless shared behavior changes |
| change a research manuscript using an already approved skill/tool | class of the manuscript/data/figure/etc. | normal execution workflow | do not classify as `PR-OPS` merely because a skill was used |

## `skill-creator` placement

Treat OpenAI `skill-creator` as a design and maintenance reference for skill lifecycle work, not as a new PR type.

When it is available, use its principles for:

- minimal skill anatomy;
- precise trigger descriptions;
- progressive disclosure;
- structural validation;
- real-task iteration.

The local playbook still controls branch/PR policy, evidence boundaries, promotion state, and workbench validation.

## Agent Reach placement

Treat Agent Reach as a third-party integration candidate under `PR-OPS`, not as a generic research or literature PR.

Use the external-agent integration workflow because adoption can change:

- local dependencies;
- network/source reach;
- credential handling;
- shell/package-manager execution;
- context volume and caching;
- external read/write capability.

Do not elevate Agent Reach to a top-level PR class. Different Agent Reach channels should be validated independently when their dependencies, credentials, or behavior differ.

## Split rule

Split skill-lifecycle changes from third-party integration adoption when they can be reviewed, validated, or rolled back independently.

Use `PR-MIX` only if one atomic change simultaneously alters the skill contract and external integration contract such that either side is unusable alone. Merely creating a companion skill for an external tool is normally two linked `PR-OPS` concerns within one PR only when the release boundary truly requires them together; otherwise split them.

## Completion criteria

- top-level class remains `PR-OPS` unless another authoritative object dictates otherwise;
- specialist workflow is selected by the changed object;
- skill creation does not bypass trigger/validation checks;
- external integration does not bypass provenance/credential/security checks;
- `PR-MIX` is not used just because more than one tool or file is involved.
