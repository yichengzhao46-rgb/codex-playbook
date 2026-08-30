# Task Routing: ChatGPT vs Codex

## Purpose

This document defines how to choose between ChatGPT and Codex for day-to-day work.

The routing rule is **not based on exclusive permissions or a claim that one tool can do something the other cannot**. Their capabilities overlap and will continue to change. Route work according to **task nature, execution environment, verification needs, interaction cost, and expected efficiency**.

GitHub is the shared source of truth for durable repository state, review, and provenance.

## Core principle

Use the tool that minimizes total work while preserving verification quality.

A useful default is:

- **ChatGPT** for understanding, deciding, synthesizing, reviewing, drafting, and interactive problem solving.
- **Codex** for repository-native implementation, repeated file operations, code execution, tests, debugging, and changes that benefit from an executable development environment.
- **Mixed workflow** when the task contains both a substantial reasoning/decision phase and a substantial implementation/verification phase.

This is a routing heuristic, not a hard capability boundary.

### Direct by default

Do not delegate merely because delegation is available.

If one environment can complete the task efficiently and verify the result to the required standard, let that environment finish the task. Escalate or hand off only when another environment materially improves correctness, execution, or review quality.

For mixed work, prefer **one deliberate handoff** over repeated ChatGPT ↔ Codex bouncing.

## Fast decision rule

Ask these questions in order:

1. **Is the main difficulty deciding what should be done?**
   - Prefer ChatGPT.
2. **Is the main difficulty making and validating changes inside a repository?**
   - Prefer Codex.
3. **Does correctness depend on running code, tests, builds, linters, scripts, or repeated edit-run-debug loops?**
   - Prefer Codex.
4. **Does the task depend on discussion, interpretation, current external information, scientific reasoning, writing quality, or comparing alternatives before acting?**
   - Prefer ChatGPT.
5. **Are both phases substantial?**
   - Use ChatGPT to frame the task and acceptance criteria, Codex to implement and verify, and GitHub PRs to record the result.
6. **Could either tool complete the task well?**
   - Choose the one with lower setup and feedback cost. Do not create a handoff merely for symmetry.

## Route by task class

Classify the task before choosing the tool. This is more stable than routing by product name, repository access, or assumed permissions.

| Task class | Default route | Main output |
| --- | --- | --- |
| Direct answer / explanation | ChatGPT | Answer, interpretation, recommendation |
| Triage / problem framing | ChatGPT | Objective, scope, acceptance criteria, route |
| Research / synthesis | ChatGPT | Evidence-backed synthesis or implementation requirements |
| Documentation-only | ChatGPT or Codex | Finished documentation with proportionate review |
| Diagnosis-only | ChatGPT or Codex | Findings without unauthorized implementation |
| Bounded code change | Codex | Working change + executable validation |
| Repository-wide / architectural change | Mixed or Codex | Approved plan + implementation + validation |
| Verification-only | Codex | Test/build/runtime evidence; no implementation unless requested |
| Review-only | ChatGPT or Codex | Findings; normally no direct repair in the same review step |
| External review feedback | Mixed | Verify finding → accept/reject → fix → re-verify |
| GitHub operation | ChatGPT or Codex | Commit, branch, PR, review action, or merge as explicitly intended |

## Decision matrix

| Task characteristic | Prefer ChatGPT | Prefer Codex | Recommended pattern |
| --- | --- | --- | --- |
| Ambiguous goal or incomplete problem definition | Strong | Weak | Clarify and frame in ChatGPT first |
| Scientific, conceptual, or methodological reasoning | Strong | Supporting | ChatGPT develops the reasoning; Codex implements resulting repo changes if needed |
| Literature/current-web synthesis or cross-source comparison | Strong | Supporting | ChatGPT synthesizes evidence, then hand off concrete changes |
| Manuscript, report, prompt, policy, or documentation drafting | Strong | Moderate | ChatGPT drafts; direct GitHub edit is acceptable when the change is small and clear |
| Small targeted repository documentation change | Strong/Moderate | Strong/Moderate | Use whichever has lower overhead; no mandatory handoff |
| Repository-wide code change or refactor | Moderate | Strong | Codex implements on a branch and validates |
| Multi-file mechanical transformation | Moderate | Strong | Codex |
| Test, build, lint, benchmark, or script execution | Weak/Moderate | Strong | Codex |
| Debugging requiring repeated local execution | Moderate | Strong | Codex edit-run-debug loop |
| Architecture or implementation trade-off before coding | Strong | Moderate | ChatGPT decides constraints; Codex implements |
| Pull request logic/content review | Strong | Strong | ChatGPT for intent/evidence/readability; Codex for implementation-level validation |
| Repetitive repository maintenance | Moderate | Strong | Codex, preferably with a reusable workflow |
| One-off explanation or learning question | Strong | Weak | ChatGPT |
| Long-running implementation with many intermediate repository states | Weak/Moderate | Strong | Codex |
| Cross-domain task combining research, writing, and repository work | Strong | Strong | Mixed workflow |

## Typical ChatGPT use cases

Prefer ChatGPT when the output is primarily a **decision, interpretation, critique, synthesis, or finished piece of writing**.

Examples:

- Decide whether a scientific claim is supported by multiple lines of evidence.
- Compare alternative manuscript structures or figure narratives.
- Review a PR for logical consistency, evidence boundaries, or documentation quality.
- Turn rough notes into a reusable rule, prompt, checklist, or policy.
- Research current external information and convert it into implementation requirements.
- Explain GitHub concepts, workflow choices, or trade-offs.
- Inspect a repository and make a small, well-scoped documentation edit when no local execution is required.

ChatGPT may also write to GitHub when the change is small, explicit, and does not benefit materially from a local execution loop. Do not route such work to Codex solely because it changes a repository.

## Typical Codex use cases

Prefer Codex when the output is primarily a **working repository change whose quality depends on execution and verification**.

Examples:

- Implement a feature across several files.
- Refactor code while preserving behavior.
- Run tests, linters, type checks, builds, or benchmarks and fix failures.
- Trace a bug through code and repeatedly edit and rerun until verified.
- Apply a mechanical transformation across many files.
- Update dependencies and resolve resulting incompatibilities.
- Build or modify scripts, notebooks, automation, CI, or repository tooling.
- Execute a previously approved implementation plan and produce a reviewable PR.

Codex should not be used merely as a second opinion when the real task is conceptual and no execution environment is needed.

## Mixed workflow

Use a mixed workflow when both reasoning and implementation are material.

Recommended sequence:

`User goal → ChatGPT framing → task envelope → Codex implementation → local validation → GitHub PR → targeted review → merge`

### Phase 1 — ChatGPT: frame the work

ChatGPT should produce only what materially reduces implementation ambiguity.

For meaningful mixed tasks, create a compact **task envelope** containing:

- objective
- acceptance criteria
- scope
- non-goals
- evidence or rationale
- risk lenses
- allowed actions or important constraints
- required output
- escalation conditions

Expected files or areas affected may be included when known, but avoid inventing implementation details that Codex can discover from the repository.

### Phase 2 — Codex: implement and verify

Codex should:

- inspect the repository before editing
- make focused changes
- run relevant validation
- review the diff
- report what was changed, what was verified, and what remains uncertain
- open or prepare a PR when the change is meaningful

### Phase 3 — GitHub: preserve state

GitHub should preserve:

- branch and commit history
- PR rationale
- review discussion
- validation evidence
- final approved version

### Phase 4 — Review with the right lens

Use ChatGPT for review questions dominated by:

- scientific or business logic
- argument quality
- evidence boundaries
- clarity and documentation
- consistency across files or claims

Use Codex for review questions dominated by:

- implementation correctness
- tests and runtime behavior
- repository conventions
- code-level regressions
- executable verification

For important changes, both reviews may be useful, but they should examine **different failure modes** rather than duplicate each other.

## Handoff discipline

A handoff should transfer a bounded task, not the entire conversation history without structure.

A useful handoff contains:

```text
Objective:
Acceptance criteria:
Scope:
Non-goals:
Relevant evidence/decisions:
Allowed actions / constraints:
Required output:
Escalate if:
```

### Single-writer rule

For one active change set, designate one primary writer at a time.

- Documentation/reasoning-heavy change: ChatGPT may be the writer.
- Implementation-heavy change: Codex should normally be the writer.
- Reviewer/tester roles should remain read-only until a finding is accepted for repair.

This avoids conflicting edits and makes provenance easier to review.

## Verification and review freshness

Validation evidence is tied to the version that was actually checked.

- Record the relevant branch/head commit when practical.
- A tracked code or test change after successful validation invalidates the previous executable verification for the affected scope.
- Re-run required tests or checks after a meaningful fix.
- Failed, blocked, or unrun checks must remain explicit; do not silently convert missing evidence into success.
- For documentation-only changes, review should be proportionate rather than forcing code-oriented gates.

For external review feedback, **verify before fixing** when the finding concerns runtime behavior, implementation correctness, or a factual claim that can be checked. Do not implement every reviewer suggestion automatically.

## Risk overrides

Small scope does not always mean low risk. Increase review/verification rigor when the task touches areas such as:

- destructive or irreversible changes
- credentials, privacy, or security boundaries
- persistent data or migrations
- dependency, build, packaging, or CI behavior
- shared helpers with broad downstream effects
- scientific data transformation, statistical analysis, or claims whose correctness depends on evidence boundaries

A risk override may upgrade a nominally simple task from direct execution to Codex verification or a Mixed workflow.

## Overlap cases

### Small documentation changes

Either ChatGPT or Codex may be efficient. Prefer ChatGPT when the content itself requires reasoning or writing judgment. Prefer Codex when the documentation update is part of a larger repository change or must be validated against many files.

### Pull requests

Both tools can participate in PR work. Do not route by the rule "ChatGPT reviews, Codex writes" or "Codex has repository permissions, ChatGPT does not." Route by the dominant work:

- PR dominated by reasoning, policy, scientific interpretation, or prose: ChatGPT may draft or edit it directly.
- PR dominated by implementation and executable validation: Codex should normally own the implementation loop.
- Mixed PR: ChatGPT defines intent and acceptance criteria, Codex implements, then the most relevant reviewer checks the result.

### Repository inspection

ChatGPT is suitable for quick inspection, explanation, comparison, and targeted changes. Codex is preferable when inspection is the start of a broader implementation/debugging session that will require many repository operations.

### Review versus repair

Keep review and repair conceptually separate:

1. identify the finding
2. verify that the finding is real and relevant
3. decide whether to accept it
4. repair if accepted
5. re-run the appropriate verification

This prevents a reviewer suggestion from becoming an unexamined code change.

## Anti-patterns

Avoid these routing rules:

- **Permission-based routing:** "Use Codex because only Codex can edit GitHub." Capabilities overlap and change.
- **Repository-based routing:** "Anything involving a repository goes to Codex." Small documentation or review tasks may be faster in ChatGPT.
- **Conversation-based routing:** "Anything discussed in chat stays in ChatGPT." Once the task becomes implementation-heavy, move it to Codex.
- **Mandatory two-tool workflow:** Do not hand off a simple task just to involve both tools.
- **Duplicate work:** Do not ask both tools to independently perform the same full task unless comparison is the explicit goal.
- **Ping-pong handoff:** Avoid repeatedly bouncing the same task between ChatGPT and Codex without a new verification need.
- **Reviewer-as-auto-fixer:** Do not treat every review comment as a command to modify the repository.
- **Stale verification:** Do not cite tests or review evidence from an earlier head after meaningful code/test changes.
- **Unverified implementation:** Do not prefer conversational convenience when correctness requires executable validation.

## Escalation thresholds

Move from ChatGPT to Codex when one or more of the following becomes true:

- the change expands beyond a few targeted files
- repeated shell or runtime checks are needed
- the task becomes an edit-run-debug loop
- repository-wide search and coordinated edits dominate the work
- tests/builds are necessary to establish correctness
- implementation state needs to persist across many steps

Move from Codex to ChatGPT when one or more of the following becomes true:

- the main blocker is no longer implementation but deciding the correct interpretation
- requirements conflict and need prioritization
- evidence must be synthesized across research, web sources, or non-code material
- the output needs substantial scientific, strategic, or writing judgment
- a reviewer must evaluate whether the implementation actually supports the intended claim or policy

Upgrade either route to Mixed when:

- a high-risk implementation depends on a non-trivial conceptual decision
- implementation correctness and evidence/claim correctness must both be independently checked
- external review findings need interpretation before code changes are accepted

## Default workflow recommendations

### Simple reasoning or writing task

`User → ChatGPT → final output`

### Small, explicit repository edit

`User → ChatGPT or Codex → GitHub commit/PR if warranted`

Choose the faster route; do not force a handoff.

### Medium or large implementation task

`User/ChatGPT requirement → Codex → tests/validation → GitHub PR → review`

### Research-to-implementation task

`User → ChatGPT research/synthesis → task envelope → Codex implementation → GitHub PR → targeted review`

### External review feedback

`Review finding → verify finding → accept/reject → Codex repair if needed → re-verify → update PR`

### High-stakes mixed task

`ChatGPT reasoning review → Codex executable validation → GitHub PR → final cross-check`

The two reviews should be complementary, not redundant.

## Minimal routing output format

When deciding where a new task should go, use this compact structure:

```text
Route: ChatGPT | Codex | Mixed
Task class: <reasoning | research | documentation | diagnosis | implementation | verification | review | mixed>
Reason: <dominant task characteristic and verification need>
ChatGPT role: <only if useful>
Codex role: <only if useful>
GitHub output: <none | commit | branch | PR>
Acceptance check: <how completion will be judged>
Escalate if: <condition that should change the route>
```

## Final rule

Do not ask "Which tool is allowed to do this?"

Ask:

> **Where is the difficult part of this task, what evidence is needed to call it complete, and which environment can produce that evidence with the least friction?**

Route based on that answer.
