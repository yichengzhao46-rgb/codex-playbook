# Pull Request Workflow

Use this workflow for meaningful Codex-generated changes.

## Default flow

1. Read repository instructions and relevant context.
2. Define one clear objective.
3. Create a task-specific branch.
4. Make the smallest complete change that satisfies the objective.
5. Run available tests, checks, or validations.
6. Review the diff for unintended edits.
7. Create a **Draft Pull Request**.
8. Summarize the change, rationale, tests, and limitations.
9. Request Codex review when appropriate.
10. Address review findings on the same branch.
11. Human approval is required before merge unless explicitly waived.

## Branch naming

Prefer concise names such as:
- `codex/add-pr-template`
- `codex/fix-parser-edge-case`
- `codex/refactor-agent-config`
- `codex/test-mcp-integration`

## PR description minimum

Every meaningful PR should include:

### Summary
What changed.

### Rationale
Why the change was needed.

### Validation
Tests, checks, or manual verification performed.

### Risks / limitations
Known gaps, assumptions, or follow-up work.

## Review focus

For code changes, review for:
- correctness
- regression risk
- edge cases
- maintainability
- security and secret handling
- reproducibility

For research-supporting code, also review for:
- data integrity
- unit handling
- replicate structure
- normalization logic
- statistical assumptions
- silent filtering or data loss

## Merge policy

Do not merge automatically by default. The PR is the checkpoint between Codex execution and human acceptance.
