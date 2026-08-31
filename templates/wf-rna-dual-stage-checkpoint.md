# WF-RNA-DUAL Stage Checkpoint

Use one copy of this template for each completed or blocked stage of the Bath–RP species-resolved transcriptomics workflow.

For figure-producing stages, this stage record must be used together with [`wf-rna-dual-figure-checkpoint.md`](wf-rna-dual-figure-checkpoint.md). A stage cannot pass while any required figure remains `NOT_STARTED`, `IN_PROGRESS`, `DRAFT_READY`, `REVISE`, `BLOCKED`, or `REOPENED` unless the user explicitly records a `WAIVED` figure with a reason.

## Workflow

- Workflow: `WF-RNA-DUAL`
- Execution repository:
- Branch / commit:
- Stage:
- Status: `NOT_STARTED | IN_PROGRESS | BLOCKED | PASS | PASS_WITH_EXCEPTION | REOPENED`
- Date:

## Figure ledger for this stage

Use `N/A` for non-figure stages.

| Figure | Status | Source-data version | User decision | Notes |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## 1. Objective completed

State the question this stage was intended to establish.

## 2. Actions performed

- scripts / tools:
- software versions:
- important parameters:
- input files / manifests:

## 3. Primary outputs

- machine-readable tables:
- figures / previews:
- figure checkpoint records:
- logs / reports:
- source-data paths:

## 4. QC / evidence summary

Record only the metrics that determine whether downstream work is safe to continue.

| Check | Result | Interpretation |
| --- | --- | --- |
|  |  |  |

## 5. Issues and decisions

Record anomalies, exclusions, ambiguous loci, sample concerns, threshold choices, figure revisions, and unresolved questions. Never omit a failed or unrun check.

## 6. Dependency impact

- Upstream artifact changed? `yes / no`
- Figures reopened if yes:
- Downstream stages to reopen if yes:
- Previous outputs invalidated:

## 7. Stage gate recommendation

Choose one:

- `PASS` — every required figure is `APPROVED` or explicitly `WAIVED`, source tables/metrics satisfy the stage gate, and the next stage may proceed;
- `REVISE` — remain in this stage and correct/re-run the current analysis or figure checkpoint;
- `BLOCK` — do not continue until required information or data are available.

Rationale:

## 8. User checkpoint

- User decision: `continue / revise / audit / stop / pending`
- Current/next figure, if the stage is still open:
- Approved exception, if any:
- Next eligible stage only if stage gate passes:
