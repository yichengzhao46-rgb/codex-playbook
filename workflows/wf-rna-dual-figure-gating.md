# WF-RNA-DUAL Figure-Level Gating

This is a mandatory companion to [`bath-rp-species-resolved-transcriptomics.md`](bath-rp-species-resolved-transcriptomics.md) whenever a `WF-RNA-DUAL` stage produces publication or supplementary figures.

Its purpose is to prevent multiple figures from being generated and interpreted at once before the user has inspected the first figure and its source data.

## Core rule

`WF-RNA-DUAL` is controlled at **two levels**:

1. **stage gate** — only one analysis stage advances at a time;
2. **figure gate** — within a figure-producing stage, only one figure advances at a time.

A stage is not `PASS` merely because its computations ran. All required figure checkpoints in that stage must be approved or explicitly waived, and the underlying source tables/metrics must satisfy the stage gate.

## Figure commands

Treat these as workflow-native commands:

- `run WF-RNA-DUAL Figure X` — generate or regenerate only Figure X from the currently valid upstream data;
- `check WF-RNA-DUAL Figure X` — read-only audit of Figure X, its source table, script, parameters, and interpretation boundary;
- `approve WF-RNA-DUAL Figure X` — record user approval for the current figure version;
- `revise WF-RNA-DUAL Figure X` — keep the figure gate open and apply only the approved revision scope;
- `rerun WF-RNA-DUAL Figure X` — regenerate the figure after an upstream or plotting change;
- `continue WF-RNA-DUAL` — if the current stage still contains an unfinished figure, advance only to the next figure checkpoint; advance to the next stage only after every required figure in the current stage is approved and the stage gate passes;
- `status WF-RNA-DUAL` — report both stage status and figure-level status.

Equivalent natural-language instructions should be interpreted the same way.

## Hard figure rules

1. Generate **one figure checkpoint at a time** unless the user explicitly authorizes a bounded batch.
2. After a figure draft is produced, stop and wait for `approve`, `revise`, `check`, `rerun`, or equivalent user instruction.
3. Do not silently proceed from one figure to the next.
4. Every figure must have a machine-readable source table or an explicit reason why the figure is schematic rather than data-derived.
5. Every data-derived figure must be reproducible from a tracked script/notebook plus recorded parameters.
6. A visual approval does not override a failed statistical, species-assignment, annotation, or evidence-boundary gate.
7. Never change the underlying analysis solely to make a figure look more convincing.
8. A figure-only aesthetic revision must not silently alter filters, data selection, statistical thresholds, normalization, or gene/module membership.
9. If upstream data, mapping, count generation, model design, or module membership changes, mark affected figures `REOPENED` even if they were previously approved.
10. Preserve the approved version or its commit reference so later changes are auditable.

## Figure status values

Use only:

- `NOT_STARTED`
- `IN_PROGRESS`
- `DRAFT_READY`
- `REVISE`
- `APPROVED`
- `BLOCKED`
- `REOPENED`
- `WAIVED`

`WAIVED` requires an explicit user decision and a reason.

## Default figure sequence

The default order is deliberately chosen so global QC and assignment checks precede mechanism-focused figures.

| Stage | Figure order | Gate logic |
| --- | --- | --- |
| 2 | `Fig. S18` | species-assignment/QC figure must be approved before Stage 3 |
| 3 | `Fig. S19` → `Fig. S20` | inspect replicate/global structure before DEG landscape |
| 4 | `Fig. 3.5a` → `Fig. 3.5b` → `Fig. S21` → `Fig. S22` | mechanism summary first, then selected genes, then complete supporting landscape |
| 5 | `Fig. 3.5c` → `Fig. S23` | Bath summary matrix first, then gene-level support |
| 6 | `Fig. S24` | ambiguity audit must pass before integrated mechanism model |
| 7 | `Fig. 3.5d` | integrated model is produced only after Stages 2–6 are valid |
| 8 | no new scientific figure by default | package/freeze only; new figures reopen the appropriate upstream stage |

The user may explicitly change the order, but the workflow should state what dependency is being bypassed and whether the change affects interpretation safety.

## Figure-specific checkpoints

### Fig. S18 — sequencing/species-assignment QC

Question: **Are sequencing quality and Bath/RP assignments reliable enough for species-resolved inference?**

Required source objects should include the per-sample counts for raw/post-filter/non-rRNA/mapped/Bath-unique/RP-unique/ambiguous/unmapped/gene-assigned reads and relevant QC metrics.

Approve only if critical failures, unexplained imbalance, and ambiguous-read burden have been reviewed.

### Fig. S19 — RP global sample structure

Question: **Are biological replicates coherent and are the planned conditions globally distinguishable without an unresolved outlier/design problem?**

Default contents: PCA, sample correlation, and hierarchical clustering.

Approval must not be interpreted as proof of a mechanism; this is a sample/design coherence checkpoint.

### Fig. S20 — RP global differential-expression landscape

Question: **What is the overall scale and distribution of the RP differential response?**

Default contents: volcano and MA plots.

Check contrast direction, FDR convention, labeling rules, and whether any labeled genes were selected post hoc for visual impact.

### Fig. 3.5a — RP pathway/module ranked enrichment

Question: **Which mechanism-relevant RP functional modules show coordinated directional transcriptional responses?**

Required checks:

- Wald-statistic or other declared ranking direction is correct;
- positive/negative direction is explicitly defined;
- module membership is auditable;
- displayed pathways are mechanism-relevant and not selected only because they are significant;
- FDR and core-enrichment metrics are correctly encoded.

### Fig. 3.5b — RP selected-gene heatmap

Question: **Do RP donor-utilization, energy/redox, and CBB-associated genes show coordinated sample-level transcriptional patterns?**

Required checks:

- all biological replicates are shown unless omission is justified;
- heatmap uses the declared transformed abundance (default VST) and gene-wise Z-score;
- `log2FC` and FDR come from the approved DE model;
- row Z-score is not called absolute/high expression;
- gene/module assignments remain traceable.

### Fig. S21 — complete enrichment landscape

Question: **Does the full enrichment result provide transparent context for the mechanism-focused subset in Fig. 3.5a?**

Approval requires consistency with the exact ranked analysis used for the main figure.

### Fig. S22 — expanded RP module heatmap

Question: **Do the broader RP functional modules support or qualify the selected-gene pattern shown in Fig. 3.5b?**

Do not use this figure to introduce a new statistical contrast without reopening Stage 4.

### Fig. 3.5c — Bath transcriptional support matrix

Question: **Are donor-side Bath functions transcriptionally represented during cocultivation?**

Required checks:

- module coverage formula is explicit;
- within-Bath expression rank/percentile is explicit;
- stable-detection rule is explicit and fixed before interpretation;
- replicate consistency is visible;
- no `upregulated`, `induced`, or `enhanced by cocultivation` language is used without a valid Bath comparator;
- Bath and RP TPM are not compared on one shared scale to imply cross-species expression strength.

### Fig. S23 — Bath gene-level support

Question: **Do the gene-level Bath TPM/coverage/consistency results transparently support the summary in Fig. 3.5c?**

Approval requires traceability from each highlighted module to its constituent genes.

### Fig. S24 — cross-species homology/ambiguity audit

Question: **Are mechanism-critical Bath/RP gene signals genuinely species-resolved?**

Prioritize CBB homologs, respiratory-chain homologs, formate/H2 genes, and any locus with notable ambiguous support.

If this figure changes species attribution or excludes a critical gene, affected Fig. 3.5a/b/c or supporting figures become `REOPENED`.

### Fig. 3.5d — integrated Bath–RP evidence model

Question: **How do species-resolved transcriptomics and independent physiological/metabolic/isotope evidence combine into the bounded methane-supported dark inorganic-carbon incorporation model?**

Required checks:

- Bath and RP use different transcriptomic encodings;
- every major arrow has an evidence class;
- candidate transfer routes remain visually distinct from directly supported connections;
- community-level EA–IRMS is not drawn as direct proof of 13C incorporation into RP;
- community ATP/NAD(H) is not silently assigned to RP;
- transcripts are not presented as proof of metabolite flux;
- no unsupported Bath induction claim appears.

## Required figure checkpoint report

For every figure, report:

1. **Figure ID and status**;
2. **Scientific question**;
3. **Upstream approved inputs**;
4. **Source table(s)**;
5. **Plotting script/notebook and key parameters**;
6. **What the figure directly shows**;
7. **What the figure does not establish**;
8. **QC/interpretation issues**;
9. **Recommendation** — `APPROVE`, `REVISE`, or `BLOCK`;
10. **Next eligible action**.

Use [`../templates/wf-rna-dual-figure-checkpoint.md`](../templates/wf-rna-dual-figure-checkpoint.md) when a persistent record is useful.

## Dependency/reopen rules

At minimum:

| Change | Reopen affected figures |
| --- | --- |
| sample identity, replicate, contrast, or batch design | S19, S20, 3.5a, 3.5b, S21, S22, and downstream integrated figures; S18 if sample set changes |
| reference or species-prefix scheme | S18 and every downstream figure |
| mapper/species-assignment rule | S18 and every downstream figure |
| count-generation/model rule | S19, S20, 3.5a, 3.5b, S21, S22, 3.5d; Bath figures if Bath quantification changes |
| RP module membership/annotation | 3.5a, 3.5b, S21/S22 as affected, S24 if homolog risk changes, 3.5d |
| Bath module membership/stable-detection threshold | 3.5c, S23, S24 if homolog risk changes, 3.5d |
| homology audit changes attribution | every figure using the affected genes plus 3.5d |
| independent metabolite/isotope/physiology evidence changes | 3.5d only unless the evidence change also affects transcriptomic interpretation |
| aesthetics only, with identical source data | current figure only; scientific stage remains valid |

## Status output example

`status WF-RNA-DUAL` should be able to report both levels, for example:

```text
Stage 4 — IN_PROGRESS

Fig. 3.5a — APPROVED
Fig. 3.5b — DRAFT_READY
Fig. S21 — NOT_STARTED
Fig. S22 — NOT_STARTED

Stage gate: not yet eligible for PASS
Next action: check Fig. 3.5b
```

## Positive case

Input: `continue WF-RNA-DUAL` while Stage 4 has Fig. 3.5a approved and Fig. 3.5b not yet started.

Expected behavior: generate/checkpoint **Fig. 3.5b only**, then stop. Do not automatically produce S21, S22, or Stage 5.

## Negative control

Input: `Make the labels on Fig. 3.5b larger.`

Expected behavior: edit/re-render Fig. 3.5b only. Do not reopen DESeq2/GSEA or generate the next figure unless the requested visual change alters data encoding.

## Maturity

Status: **experimental / specification-complete, not yet forward-validated on the user’s actual transcriptome dataset**.

Promote together with `WF-RNA-DUAL` only after a real-data run demonstrates that figure gating prevents premature downstream work without creating excessive manual overhead.