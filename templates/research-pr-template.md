# Research PR Template

Remove sections and checklist rows that do not apply.

```markdown
## Summary

- Project key: `<GENERAL|POLYU|ELC|ZOTERO|DATA|FIG|ORIGIN|DOCS|CODEX>`
- Primary PR class: `<PR-RSCH|PR-LIT|PR-DATA|PR-FIG|PR-ORG|PR-DOC|PR-OPS|PR-MIX>`
- Constituent classes, if `PR-MIX`:
- Scenario:
- Change:

## Rationale

-

## Authoritative object(s)

-

## Changed files

- `path`:

## Workflow coverage

| Class | Area | Source of truth | Validation | Status |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## Validation

- [ ] Skill, agent, or routing validation:
- [ ] Data or source validation:
- [ ] Visual or render QA:
- [ ] Zotero storage/index QA:
- [ ] Word/PDF structural QA:
- [ ] Regression or smoke test:
- [ ] If `PR-MIX`, all constituent validation gates applied:

## Evidence boundaries

- Directly verified:
- Source-backed but not reproduced:
- Inferred or analogy-based:
- Not checked:

## Risks and rollback

- Risk:
- Rollback:
- If `PR-MIX`, why splitting is not viable:

## Follow-up

-
```
