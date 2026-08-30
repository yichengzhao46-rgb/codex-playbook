# Skill Lifecycle Workflow

Use this specialist workflow under `PR-OPS` when creating, updating, validating, promoting, or deprecating a reusable Codex skill.

This workflow is informed by the official OpenAI `skill-creator` design principles, but the local playbook remains authoritative for routing, review, validation, and promotion.

## Why this remains `PR-OPS`

The authoritative object is a reusable skill or skill-maintenance method. Do not create a separate PR class for skill creation merely because the skill later supports research, figures, documents, data, or another domain.

Use a secondary class checklist only when the change itself materially modifies another authoritative object.

## Stage 1 — Define the skill contract

Before creating files, record:

- skill name;
- concrete user/task trigger;
- non-trigger cases;
- expected inputs;
- expected outputs;
- tools or external dependencies;
- safety or approval boundaries;
- validation evidence required before stable promotion.

Prefer one coherent capability over a broad catch-all skill.

## Stage 2 — Design for progressive disclosure

Keep always-loaded metadata concise and make the trigger description precise enough to determine when the skill should be used.

Use the skill body for the operational workflow after triggering. Put optional long-form references, scripts, and reusable assets in separate resources so they are loaded or executed only when needed.

Avoid adding auxiliary documentation that does not help a future agent perform the task.

## Stage 3 — Skill anatomy and metadata gate

At minimum, verify that the skill has:

- a required `SKILL.md`;
- valid frontmatter required by the current Codex skill format;
- a clear name;
- a description that states both what the skill does and the important trigger contexts;
- imperative, operational instructions rather than retrospective notes;
- only the bundled resources actually needed for execution.

When an interface metadata file is used, keep it synchronized with the skill's actual purpose and default prompt behavior.

## Stage 4 — Trigger quality review

Test the description against representative cases.

Require at least:

- one positive trigger that should select the skill;
- one nearby negative control that should not select it;
- one ambiguity case when the skill overlaps another router or specialist.

Refine the description before adding routing exceptions elsewhere. Do not compensate for a vague trigger by creating duplicated global routers.

## Stage 5 — Structural validation

Run the available skill validator or equivalent structural check.

Check at least:

- frontmatter syntax;
- required fields;
- naming rules;
- missing referenced resources;
- placeholder/example content that should have been replaced;
- stale paths or environment-specific assumptions;
- source-versus-installed copy drift where relevant.

Record what was actually validated. Do not claim tool execution or installation success unless it was performed.

## Stage 6 — Real-task validation

A structurally valid skill is not automatically a useful skill.

Test it on at least one realistic task when practical and evaluate:

- whether it triggered at the right time;
- whether it loaded unnecessary context;
- whether instructions were sufficient without hidden assumptions;
- whether tool calls followed the intended safety boundary;
- whether the output met the task contract;
- whether another existing skill already covers the same job better.

Use `codex-workbench` for controlled forward validation when the behavior is reusable or easy to over-apply.

## Stage 7 — Iteration and promotion

Classify the skill state as:

- `experimental` — structure exists but real-task behavior is not adequately validated;
- `validated` — representative real-task evidence exists within a bounded scope;
- `stable` — repeated use supports the intended trigger and workflow with known limitations;
- `deprecated` — superseded, unsafe, misleading, or no longer maintained.

Promotion should be evidence-matched. One successful task does not prove universal trigger quality.

## Update rule

When a real task exposes a struggle or inefficiency:

1. identify whether the problem came from triggering, instructions, resources, tooling, or the external environment;
2. make the smallest reusable fix;
3. re-run the affected positive and negative cases;
4. record any newly discovered non-trigger or failure mode;
5. update promotion status only if the new evidence supports it.

## PR requirements

A meaningful skill PR should state:

- skill purpose and trigger;
- authoritative source location;
- files/resources changed;
- positive trigger case;
- negative control;
- structural validation performed;
- real-task validation performed or explicitly not performed;
- known overlap with other skills;
- installation/source synchronization status when relevant;
- rollback or deprecation path.

## Completion criteria

A skill-lifecycle change is ready for human review when:

- the trigger is explicit and bounded;
- the skill structure is valid;
- duplicated routing has been checked;
- positive and negative behavior are documented for meaningful trigger changes;
- real-task evidence is distinguished from structural validation;
- source/install drift is explicit where applicable;
- secrets, credentials, and private data are absent;
- promotion status matches the evidence.
