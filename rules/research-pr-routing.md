# Research PR Routing Rules

Use these rules to classify reviewable changes to recurring research and Codex
workflows. Explicit task intent outranks the current directory name.

## Scope gate

Apply this routing only when the user requests PR packaging, merge review,
release notes, or a reviewable workflow change package. An ordinary paragraph
revision, literature lookup, calculation, figure export, or market brief remains
in its execution workflow.

If that work changes a reusable script, skill, rule, template, agent, or
configuration, classify the changed object here.

## Project and scenario routes

| Project key | Typical artifacts or scenarios | Primary PR class | Primary execution route |
| --- | --- | --- | --- |
| `POLYU` | Bath-RP, MOB-EET, confirmation report, thesis chapters, mechanism or evidence synthesis | `PR-RSCH` | Research or writing specialist |
| `ELC` | CARS outline, academic paragraph, local rubric, cohesion or tone workflow | `PR-RSCH` | Outline or paragraph revision specialist |
| `ZOTERO` | DOI records, PDFs/SI, classification, attachment repair, citation mapping, evidence mining | `PR-LIT` | Zotero-first literature specialist |
| `DATA` | CSV/Excel, qPCR, isotope, EEM/FRI, calibration, statistics, figure-ready tables | `PR-DATA` | Data analysis specialist |
| `FIG` | Manuscript plots, schematics, existing figure inspection, raster-local edits, journal exports | `PR-FIG` | Figure, inspection, or schematic specialist |
| `ORIGIN` | Native workbook/graph, editable `.opju`, preview, legend/axis/color refinement | `PR-ORG` | Origin refinement specialist |
| `DOCS` | DOCX, PDF, rendering, redlining, comments, tracked changes, document structure | `PR-DOC` | Native document or PDF specialist |
| `CODEX` | Skills, agents, MCP/plugin rules, routing, token optimization, installation or synchronization | `PR-OPS` | Skill maintainer or routing auditor |

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
and separating them would make either part unusable. Split changes when they
have different owners, validation methods, rollback paths, or release timing.

Common split candidates include:

- data calculation versus manuscript wording
- Zotero import/classification versus chapter revision
- reusable plotting workflow versus one project figure
- Word renderer repair versus substantive document edits

## Compact invocation card

Retain this card before loading detailed checklists:

```text
Project key:
Scenario:
Primary PR class:
Secondary checklist, if required:
Execution specialist:
Authoritative source:
Expected validation:
Split or combined:
```
