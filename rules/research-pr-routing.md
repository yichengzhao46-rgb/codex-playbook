# Research PR Routing Rules

Use these rules to classify reviewable changes to recurring research and Codex
workflows.

## Scope gate

Apply this routing only when the user requests PR packaging, merge review,
release notes, or a reviewable workflow change package. An ordinary paragraph
revision, literature lookup, calculation, figure export, or market brief remains
in its execution workflow.

If that work changes a reusable script, skill, rule, template, agent, or
configuration, classify the changed object here.

## Generic PR class taxonomy

The PR class is determined by the authoritative object being changed. This
classification is reusable across projects and should remain stable even when
personal project names change.

| PR class | Authoritative object |
| --- | --- |
| `PR-RSCH` | manuscript, chapter, academic argument, or research-writing method |
| `PR-LIT` | literature library, evidence table, search method, citation mapping, or attachment workflow |
| `PR-DATA` | data-processing script, calculation, statistical logic, calibration, or analysis table |
| `PR-FIG` | figure source, visual semantics, layout, annotation, or publication export workflow |
| `PR-ORG` | Origin-native workbook, graph, editable `.opju`, or Origin refinement workflow |
| `PR-DOC` | Word/PDF structure, rendering, tracked changes, comments, pagination, or document workflow |
| `PR-OPS` | Codex skill, agent, MCP/plugin rule, router, template, configuration, or operating workflow |
| `PR-MIX` | one atomic change spanning multiple authoritative objects that cannot be separated without making the change unusable |

## Personal project routing profile

The following project keys are personal routing aliases for recurring work. They
suggest a likely execution route and default PR class, but they do **not** define
the generic taxonomy and must not override the authoritative changed object.

| Project key | Typical artifacts or scenarios | Default PR class | Primary execution route |
| --- | --- | --- | --- |
| `POLYU` | Bath-RP, MOB-EET, confirmation report, thesis chapters, mechanism or evidence synthesis | `PR-RSCH` | Research or writing specialist |
| `ELC` | CARS outline, academic paragraph, local rubric, cohesion or tone workflow | `PR-RSCH` | Outline or paragraph revision specialist |
| `ZOTERO` | DOI records, PDFs/SI, classification, attachment repair, citation mapping, evidence mining | `PR-LIT` | Zotero-first literature specialist |
| `DATA` | CSV/Excel, qPCR, isotope, EEM/FRI, calibration, statistics, figure-ready tables | `PR-DATA` | Data analysis specialist |
| `FIG` | Manuscript plots, schematics, existing figure inspection, raster-local edits, journal exports | `PR-FIG` | Figure, inspection, or schematic specialist |
| `ORIGIN` | Native workbook/graph, editable `.opju`, preview, legend/axis/color refinement | `PR-ORG` | Origin refinement specialist |
| `DOCS` | DOCX, PDF, rendering, redlining, comments, tracked changes, document structure | `PR-DOC` | Native document or PDF specialist |
| `CODEX` | Skills, agents, MCP/plugin rules, routing, token optimization, installation or synchronization | `PR-OPS` | Skill maintainer or routing auditor |

Use `GENERAL` when no personal project key is needed.

## Routing precedence

When signals disagree, apply this precedence:

1. Explicit user intent defines the requested scope and deliverable.
2. The authoritative changed object determines the primary PR class.
3. A personal project key suggests the default specialist or workflow only.
4. Directory name or current working location is a weak fallback signal.

Example: a `POLYU` task that changes a reusable statistical calculation script is
`PR-DATA`, not `PR-RSCH`, because the changed authoritative object is the data
analysis logic.

## Class selection

- Classify by the authoritative object being changed, not every artifact created
  during validation.
- A data script that exports a QA plot remains `PR-DATA` unless figure semantics,
  style, layout, or annotations also changed.
- An Origin-native deliverable is `PR-ORG`; add `PR-DATA` only when calculation
  or statistical logic changed.
- Manuscript prose supported by Zotero evidence is `PR-RSCH`. Use `PR-LIT` when
  the library, search method, attachments, citation mapping, or evidence table is
  the changed deliverable.
- A Word renderer is `PR-DOC`. A general Codex skill that routes Word tasks is
  `PR-OPS` with `PR-DOC` as a secondary checklist.
- A figure embedded in Word is `PR-FIG` when the figure source changed and
  `PR-DOC` when only placement, pagination, captions, or rendering changed.

## Split versus mixed

Choose one primary class. Add a secondary checklist only for a genuine
cross-boundary dependency.

Use `PR-MIX` only when one atomic change affects multiple authoritative objects
and separating them would make either part unusable. A `PR-MIX` package must
name every authoritative object involved, explain why splitting is not viable,
and apply the validation gates for every constituent class. It must not be used
to bypass a class-specific validation requirement.

Split changes when they have different owners, validation methods, rollback
paths, or release timing.

Common split candidates include:

- data calculation versus manuscript wording
- Zotero import/classification versus chapter revision
- reusable plotting workflow versus one project figure
- Word renderer repair versus substantive document edits

## Compact invocation card

Retain this card before loading detailed checklists:

```text
Project key or GENERAL:
Scenario:
Primary PR class:
Secondary checklist, if required:
Execution specialist:
Authoritative source:
Expected validation:
Split or combined:
```
