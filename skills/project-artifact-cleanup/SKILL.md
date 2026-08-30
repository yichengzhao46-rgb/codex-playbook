---
name: project-artifact-cleanup
purpose: Safely inventory, classify, stage, archive, and optionally delete obsolete project files, preview renders, temporary artifacts, caches, and superseded versions without risking source data or current authoritative files.
primary_route: Codex
primary_pr_class: PR-OPS
status: experimental
version: 0.1
validation_status: controlled forward validation pending
---

# Project Artifact Cleanup

## Purpose

Use this Skill when a user wants Codex to clean a project/workspace folder containing old versions, temporary outputs, preview renders, intermediate files, caches, duplicate exports, or other low-value artifacts while preserving source files, research data, current deliverables, and repository integrity.

The default objective is **workspace hygiene with reversibility**, not maximum deletion.

## Automatic trigger

Trigger this Skill when the user asks to:

- clean up a project folder or workspace;
- remove old, temporary, preview, rendered, test, cache, or intermediate files;
- identify files that are safe to delete;
- archive superseded versions while retaining current versions;
- clean Codex-generated preview/render artifacts;
- reduce clutter without risking important source files;
- produce a deletion manifest before removing files.

## Do not trigger

Do not use this Skill when:

- the user already names exact files to delete and no classification is needed;
- the task is ordinary Git branch cleanup, dependency cleanup, package-manager cache cleanup, or system-wide disk cleanup;
- the user wants data deduplication based on scientific content rather than file provenance;
- the user asks to reorganize a research dataset schema rather than clean artifacts;
- a domain-specific retention policy, legal hold, institutional archive rule, or regulated-data policy controls deletion and has not been supplied.

For exact-file deletion, follow the user's explicit scope and normal safety rules. For regulated retention, stop and request the governing policy before destructive action.

## Core principles

### 1. Inventory before action

The first pass is always read-only.

Do not delete, move, rename, overwrite, or modify files during the initial inventory.

Record, when available:

- path;
- file type;
- size;
- modification time;
- Git tracked/untracked/ignored state;
- likely role;
- whether referenced by project files, scripts, README, manifests, or workflows;
- whether a newer authoritative version exists;
- whether the file can be deterministically regenerated from retained sources.

### 2. Four-way classification

Classify every candidate into exactly one primary category:

#### KEEP

Use for files that are current, authoritative, irreplaceable, or needed to reproduce work.

Examples:

- raw/source research data;
- current manuscript/report/spreadsheet/presentation;
- current figure source files;
- Origin/project source files;
- original images;
- analysis scripts/notebooks;
- configuration, README, workflow, rule, skill, or repository metadata;
- final submission-quality outputs when they are part of the deliverable;
- files whose purpose or reconstructability makes deletion unsafe.

#### SAFE-DELETE

Use only when there is high confidence the file has no continuing authoritative value and is safely reconstructable or disposable.

Typical examples:

- document-page preview renders;
- temporary PNG/JPG/WebP generated only for visual inspection;
- temporary PDFs generated only for preview/QA;
- cache/temp/scratch/debug outputs;
- duplicate intermediate exports;
- rendering directories that can be regenerated from retained source files;
- test outputs that are not fixtures, baselines, or validation evidence.

Filename patterns such as `preview`, `render`, `tmp`, `temp`, `scratch`, `debug`, `test`, `_old`, `_copy`, or `_backup` are **signals only**, never sufficient proof by themselves.

#### ARCHIVE

Use for superseded files that may still have historical, provenance, or recovery value.

Examples:

- earlier manuscript/report versions;
- prior figure versions;
- superseded analysis outputs used in past interpretation;
- previous deliverables that may be useful for traceability.

Do not classify an old file as SAFE-DELETE merely because a newer version exists.

#### REVIEW

Use whenever purpose, provenance, dependency, authorship, or recoverability is unclear.

Ambiguity defaults to REVIEW, not deletion.

### 3. Regenerability test

Ask:

> Can this file be deterministically regenerated from retained authoritative sources using an available or standard workflow without losing unique information?

If **yes**, the file may move toward SAFE-DELETE if no other dependency or archival reason exists.

If **no** or uncertain, prefer KEEP, ARCHIVE, or REVIEW.

Regenerability is not sufficient by itself: a final submission artifact may still belong in KEEP even if reproducible.

### 4. Source-data protection

Never classify raw/source research data as SAFE-DELETE merely because derived summaries or later exports exist.

Examples requiring strong protection include:

- original instrument exports;
- raw sequencing or microscopy data;
- original spreadsheets containing replicate-level values;
- unprocessed images;
- unique source documents;
- files needed to reproduce quantitative results.

If the same data exist in several representations, inspect units, normalization, denominators, formulas, timestamps, and provenance before calling one redundant.

### 5. Git-aware behavior

If the workspace is inside a Git repository:

1. inspect `git status` before cleanup;
2. distinguish tracked, untracked, and ignored files;
3. treat tracked files as higher-risk than untracked disposable artifacts;
4. never use a broad destructive command as a substitute for classification;
5. do not use `git clean -fdx` in this workflow;
6. do not use `rm -rf *` or an equivalent broad wildcard deletion;
7. do not delete uncommitted work merely because it is untracked;
8. if `git clean` is useful for inspection, use dry-run behavior first and treat its output only as one signal, not an automatic deletion list.

A tracked file can still be obsolete, but removal must be explicit in the manifest and should normally be represented as a reviewed repository change.

### 6. First-pass dry-run gate

The first-pass output must include a cleanup table:

| File | Category | Reason | Git state | Regenerable? | Dependency / provenance note | Proposed action |
| --- | --- | --- | --- | --- | --- | --- |

Also report:

- total files inspected;
- candidate count by category;
- estimated space associated with SAFE-DELETE;
- likely Codex-generated preview/render artifacts;
- any high-risk or ambiguous items.

Then **stop for user approval** before moving or deleting anything.

### 7. Reversible cleanup stage

After approval, prefer reversible movement over permanent deletion.

Default destinations:

```text
_cleanup_staging/YYYY-MM-DD/
_archive/
```

Rules:

- SAFE-DELETE candidates move to `_cleanup_staging/YYYY-MM-DD/` first;
- ARCHIVE candidates move to `_archive/` if the user approved archival movement;
- preserve relative paths where practical;
- KEEP and REVIEW remain untouched;
- if a candidate changed since the dry-run, remove it from the action set and reclassify it as REVIEW;
- do not silently expand the approved manifest.

If the environment provides a native recoverable Trash/Recycle Bin mechanism and it is safer than project-local staging, that may be used instead, but report which recovery path was used.

### 8. Post-clean verification

After staging/archive operations, verify:

- current authoritative files still exist;
- raw/source research data still exist;
- current figure/document/project source files still exist;
- relevant project references are not obviously broken;
- Git status is understood and consistent with the approved actions;
- no REVIEW item was moved;
- no file outside the approved manifest was changed.

Report:

```text
Staged for possible deletion:
Archived:
Preserved:
Skipped / reclassified to REVIEW:
Estimated space isolated:
Git status before:
Git status after:
```

### 9. Permanent deletion requires a second manifest

Do not permanently delete staged files merely because the staging step succeeded.

Before permanent deletion:

1. rescan the staging area;
2. confirm each file is still unreferenced or safely superseded;
3. confirm it is not raw/source data;
4. confirm it is not the only copy of a unique source;
5. confirm the user has had an opportunity to validate the project after staging;
6. produce a **final deletion manifest**;
7. obtain explicit user approval for that manifest.

Permanent deletion must be restricted to exactly the approved manifest.

### 10. Changed-since-review protection

A file that was modified, replaced, or newly referenced after the dry-run or staging decision must be removed from the deletion set until it is reviewed again.

This protects against stale manifests.

## Old-version decision rule

Do not infer supersession from names alone.

For sequences such as:

```text
report_v1.docx
report_v2.docx
report_v3.docx
report_v3_typography.docx
```

consider:

- modification history;
- Git history/state;
- whether a file is a true predecessor or a divergent branch;
- whether later versions preserve all unique information;
- whether comments, tracked changes, annotations, or embedded objects differ;
- whether the older file was cited or used as a source for later work.

Default old research documents to ARCHIVE unless there is strong evidence they are disposable duplicates.

## Common classification examples

| Example | Default classification | Rationale |
| --- | --- | --- |
| `rendered/page_01.png` from DOCX QA | SAFE-DELETE | regenerable preview artifact |
| `report_preview.pdf` | SAFE-DELETE | preview-only derivative |
| `figure_test.png` | SAFE-DELETE or REVIEW | disposable if clearly test-only and unreferenced |
| `figure_final_600dpi.tif` | KEEP | formal deliverable |
| `figure.opju` | KEEP | authoritative editable source |
| `raw_data.xlsx` | KEEP | source research data |
| `report_v1.docx` after v3 exists | ARCHIVE | superseded but historically valuable |
| unknown `.csv` | REVIEW | ambiguous role/provenance |
| tracked obsolete fixture | REVIEW / reviewed removal | tracked status raises risk; may be intentional test evidence |

## External benchmark principles adapted locally

This Skill adopts or adapts the following general patterns:

- **Git dry-run before cleanup:** Git's cleanup tooling explicitly supports inspection before action; locally adapted into a full inventory/classification gate rather than treating Git's candidate list as authoritative.
- **Recoverable deletion before permanent erasure:** desktop Trash/Recycle Bin conventions separate reversible removal from permanent deletion; locally adapted into `_cleanup_staging/` plus a second deletion manifest.
- **Research-data retention and versioning:** research data-management practice favors preserving raw/source data and retaining traceable prior versions when provenance matters; locally adapted into KEEP for source data and ARCHIVE for superseded research artifacts.

Rejected patterns:

- broad automatic deletion based only on ignored/untracked status;
- filename-only cleanup heuristics;
- permanent deletion in the first pass;
- treating every old version as disposable;
- system-wide cleanup behavior inside a project-focused Skill.

## Execution route and PR behavior

The Skill itself is a reusable operating method and changes to it are `PR-OPS`.

When the Skill is used in another repository, the actual PR class depends on the authoritative objects changed. Cleaning only disposable untracked previews may require no GitHub PR. Removing tracked project files is a repository change and should follow the applicable PR classification and review rules.

## Validation status

Status: **experimental**.

Required before promotion:

- positive case: mixed project directory containing current source files, raw data, old versions, preview renders, temp files, tracked fixtures, and ambiguous files;
- negative control: exact-file deletion request where no classification workflow is needed;
- ambiguity test: an old-looking file that is still referenced or is the only editable source;
- acceptance check: zero source/raw/current files classified as SAFE-DELETE, all ambiguous items routed to REVIEW, and preview/temp artifacts correctly identified without broad destructive commands.
