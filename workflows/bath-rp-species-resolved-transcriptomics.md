# Bath–RP Species-Resolved Transcriptomics Workflow

Use this workflow for transcriptomic analysis of the defined *Methylococcus capsulatus* Bath–*Rhodopseudomonas palustris* coculture when the goal is to connect Bath donor-side metabolism with RP recipient-side energy/redox responses and CBB-associated dark inorganic-carbon assimilation without exceeding the evidence supported by bulk RNA-seq and community-level isotope measurements.

This is a reusable analysis method. Project-specific FASTQ files, reference genomes, count matrices, figures, and outputs belong in the relevant execution/project repository, not in `codex-playbook`.

## Workflow key and invocation

Canonical workflow key: `WF-RNA-DUAL`

### Default staged behavior

`run WF-RNA-DUAL` **starts Stage 0 only**. It must not silently execute the complete analysis.

Useful commands:

- `run WF-RNA-DUAL` — start or resume the workflow at the first unfinished stage;
- `run WF-RNA-DUAL Stage N` — execute only the named stage;
- `check WF-RNA-DUAL Stage N` — perform a read-only audit of that stage and its outputs;
- `status WF-RNA-DUAL` — report the stage ledger, current blockers, and next eligible stage;
- `continue WF-RNA-DUAL` — execute only the next stage after the preceding stage has passed its gate;
- `rerun WF-RNA-DUAL Stage N` — rerun a stage after an approved correction;
- `stop WF-RNA-DUAL after Stage N` — explicitly limit the current task to that stage.

Treat equivalent natural-language requests as the same workflow. Do not trigger the workflow for single-gene RT-qPCR, ordinary single-species RNA-seq, metagenomics, or manuscript wording review that does not require transcriptomic re-analysis.

## Primary objective

Produce a reproducible, species-resolved analysis that supports the following evidence chain:

`Bath methane oxidation and donor-side metabolic capacity → candidate diffusible products / reducing equivalents → RP donor utilization and respiratory energy conservation → RP CBB-associated transcriptional response → consistency with enhanced community-level inorganic-carbon incorporation`

The workflow must support this chain without claiming that transcriptomics alone proves metabolite flux, species-specific isotope incorporation, or induction of Bath pathways in the absence of a Bath-only transcriptomic comparator.

## Stage-control contract

This workflow is deliberately **stage-gated** so the user can inspect, challenge, revise, or stop the analysis before downstream interpretation is built on a weak upstream result.

### Hard rules

1. Execute **one stage at a time** unless the user explicitly authorizes a bounded multi-stage run.
2. At the end of every stage, stop and present a checkpoint report before continuing.
3. A stage may advance only when its gate is `PASS` or the user explicitly accepts a documented exception.
4. Never hide failed QC by continuing into downstream analyses.
5. Never exclude a sample, gene family, homologous locus, or replicate silently.
6. If an upstream artifact changes, mark dependent downstream stages `REOPENED` and rerun the affected work.
7. Keep stage outputs machine-readable and traceable to scripts, parameters, software versions, and the relevant commit.
8. A visual figure is not sufficient proof that a stage passed; retain the source table and validation metrics.

### Stage status values

Use only:

- `NOT_STARTED`
- `IN_PROGRESS`
- `BLOCKED`
- `PASS`
- `PASS_WITH_EXCEPTION`
- `REOPENED`

Maintain a stage ledger in the execution repository, preferably from `templates/wf-rna-dual-stage-checkpoint.md`.

### Required end-of-stage checkpoint report

After each stage report:

1. **Objective completed** — what this stage was supposed to establish;
2. **Actions performed** — tools/scripts and important parameters;
3. **Primary outputs** — files, tables, and figures created;
4. **QC / evidence summary** — the metrics that matter for deciding whether to continue;
5. **Issues and decisions** — anomalies, exclusions, ambiguity, or unresolved questions;
6. **Gate recommendation** — `PASS`, `REVISE`, or `BLOCK`, plus the next eligible stage.

Then stop and wait for the user to continue, revise, or audit.

## Default execution route

This is normally a `PR-DATA` task with scientific interpretation constraints.

- **Codex**: primary executor for repository-native pipeline construction, combined-reference preparation, mapping, quantification, DESeq2/GSEA scripts, figure generation, reproducibility, and validation.
- **ChatGPT**: framing, pathway/module curation, literature/database interpretation, evidence-boundary review, and final figure/manuscript reasoning.
- **GitHub**: versioned source of truth for scripts, parameters, manifests, stage ledger, analysis notes, validation evidence, and PR review.
- **Optional specialist plugins**: NGS Analysis Workbench, Biological Sequence & Alignment Viewer, Life Sciences Databases, and Life Sciences Literature may be used for cross-checking or specialist inspection when available. They are not required for completion and must not become hidden dependencies.

Use one primary writer at a time. If Codex is executing the analysis, ChatGPT should review requirements/results rather than editing the same active files concurrently.

# Stage map

| Stage | Name | Main question | Main outputs | Hard gate |
| --- | --- | --- | --- | --- |
| 0 | Intake and analysis freeze | Are the samples, contrasts, references, and scope correct? | sample sheet, analysis contract, input manifest | user-approved design |
| 1 | Combined reference and provenance | Can Bath and RP be distinguished against an auditable reference? | combined reference, ID map, reference manifest | species-unique IDs and traceable references |
| 2 | Sequencing QC and competitive species assignment | Are the reads and species assignments reliable enough to proceed? | QC table, MultiQC-style report, Fig. S18 source data | no unexplained critical QC/species-assignment failure |
| 3 | Quantification and RP global differential structure | Is the RP comparison statistically and biologically coherent? | RP counts, DESeq2, PCA/correlation, volcano/MA, Figs. S19–S20 | valid design and acceptable replicate structure |
| 4 | RP mechanism-oriented functional response | Does RP show coordinated donor-use, energy/redox, and CBB responses? | GSEA/modules, Fig. 3.5a–b, Figs. S21–S22 | curated modules and directionality validated |
| 5 | Bath donor-side transcriptional support | Are donor-side Bath functions transcriptionally represented during coculture? | Bath TPM/ranks/coverage, Fig. 3.5c, Fig. S23 | descriptive-only interpretation and stable module definitions |
| 6 | Cross-species homology and ambiguity audit | Are mechanism-critical genes genuinely species-resolved? | Fig. S24, homology/ambiguity audit | critical ambiguous loci resolved, excluded, or downgraded |
| 7 | Cross-omics integration and mechanistic model | Do transcriptomics and independent evidence form a coherent bounded model? | Fig. 3.5d, evidence matrix | every edge has an explicit evidence level |
| 8 | Final package and manuscript handoff | Is the analysis reproducible, traceable, and publication-ready? | final figures/tables/scripts/manifests/method notes | complete provenance and unresolved limits documented |

---

# Stage 0 — Intake and analysis freeze

## Goal

Freeze the biological design before any downstream computation creates momentum around an incorrect sample map or contrast.

## Required inputs

Resolve or explicitly mark missing:

1. raw or cleaned FASTQ files for every biological replicate;
2. sample metadata with condition, replicate, library layout, strandedness if known, sequencing batch if applicable, and any other design factor that could affect the model;
3. authoritative Bath reference genome and annotation;
4. authoritative RP reference genome and annotation;
5. expected sample groups, including the RP-only versus coculture comparison used for RP differential expression;
6. confirmation that Bath lacks an equivalent Bath-only RNA-seq comparator unless new data are supplied;
7. target output scope: Fig. 3.5a–d, Figs. S18–S24, tables, or a subset.

Do not infer ambiguous sample identities from filenames alone.

## Actions

- build and review the sample sheet;
- verify biological replicates and contrast direction;
- record library layout/strandedness and batch variables;
- identify reference accessions/versions to be used;
- freeze the initial software/pipeline plan at the level needed for reproducibility;
- create the workflow stage ledger.

## Outputs

- `samplesheet.tsv` or equivalent;
- `analysis_contract.md` describing contrast, scope, non-goals, and evidence limits;
- input/reference manifest;
- stage ledger with Stage 0 marked `IN_PROGRESS` then `PASS` only after approval.

## Gate 0

`PASS` only when the user can answer yes to:

- sample identities are correct;
- biological replicates are correct;
- RP comparison direction is explicit;
- Bath comparator status is explicit;
- reference versions are identified;
- target deliverables are agreed.

If not, remain in Stage 0.

---

# Stage 1 — Combined reference and provenance

## Goal

Create the auditable reference required for competitive Bath/RP species assignment.

## Actions

- concatenate authoritative Bath and RP genomes and compatible annotations;
- add unambiguous species prefixes to sequence, gene, transcript, and feature identifiers where needed;
- preserve an ID map back to original annotations;
- record accessions, versions, download dates, checksums when practical, and annotation transformations;
- build required indices;
- create a preliminary list of obvious cross-species homolog families that may require later targeted auditing.

Preferred principle: competitive assignment against the combined reference rather than sequentially mapping first to one species and then the other.

## Outputs

- combined FASTA and annotation;
- species-prefix / original-ID mapping table;
- reference manifest;
- index-generation log;
- preliminary homolog-risk list.

## Gate 1

`PASS` only when:

- all reference identifiers are species-unambiguous;
- original IDs remain recoverable;
- the exact source references are recorded;
- index creation succeeds;
- no silent annotation collisions remain.

A reference change after Stage 1 reopens Stages 2–8.

---

# Stage 2 — Sequencing QC and competitive species assignment

## Goal

Determine whether raw sequencing quality and Bath/RP assignment are reliable enough for species-resolved inference.

## Actions

For each sample record at minimum:

`raw reads → post-filter reads → non-rRNA reads → mapped reads → Bath uniquely assigned → RP uniquely assigned → ambiguous/multimapped → unmapped → gene-assigned reads`

Also inspect where applicable:

- base quality and adapter metrics;
- read length and library layout;
- duplication/library-complexity signals;
- inferred versus expected strandedness;
- rRNA fraction;
- mapping rate;
- species-assignment proportions;
- unexpected contamination or extreme species imbalance;
- preliminary ambiguous-mapping burden.

The exact mapper/quantifier may be selected according to the execution environment, but the choice and parameters must be recorded and applied consistently.

## Outputs

- per-sample QC/species-assignment table;
- aggregated QC report;
- Fig. S18 source table and figure draft;
- list of samples or loci requiring attention.

## Gate 2

`PASS` only when:

- no sample has an unexplained critical QC failure;
- mapping and gene-assignment rates are interpretable;
- Bath/RP unique assignment is explicitly quantified;
- ambiguous/multimapped reads are quantified rather than hidden;
- any extreme sample/species imbalance has been reviewed;
- no sample is excluded without an explicit decision record.

If species assignment is not reliable, stop here. Do not proceed to DEG or pathway interpretation.

---

# Stage 3 — Quantification and RP global differential structure

## Goal

Generate species-resolved count matrices and test whether the RP-only versus coculture comparison is statistically coherent before mechanism-focused interpretation.

## Actions

### RP

- retain raw integer gene counts for DESeq2;
- generate descriptive TPM only if useful for abundance checks;
- fit the user-approved DESeq2 model or equivalently justified count-based model;
- retain `baseMean`, `log2FoldChange`, `lfcSE`, Wald statistic, raw P value, and BH-adjusted P value/FDR;
- use VST or another justified transformation for PCA, correlation, clustering, and heatmap visualization.

### Bath

- generate raw counts and TPM or another explicitly documented within-sample abundance metric for later Stage 5;
- do not perform Bath coculture-versus-monoculture DE unless a valid comparator exists.

### Global RP QC

Prepare:

- PCA;
- sample correlation matrix;
- hierarchical clustering;
- volcano plot;
- MA plot.

## Outputs

- species-resolved count matrices;
- full RP DESeq2 table;
- Bath raw-count/TPM table for later stages;
- Fig. S19: RP PCA/correlation/clustering;
- Fig. S20: RP volcano/MA.

## Gate 3

`PASS` only when:

- DESeq2 receives unnormalized integer counts;
- the model matches the frozen biological design;
- replicate structure is acceptable or any outlier decision is explicitly documented;
- contrast direction is verified;
- VST/TPM are not misused as DESeq2 inference input;
- global results do not reveal a design or sample problem that invalidates the comparison.

A sample-removal or design change reopens Stage 3 and all downstream analytical stages.

---

# Stage 4 — RP mechanism-oriented functional response

## Goal

Test whether RP exhibits a coordinated transcriptional response in donor utilization, energy/redox conservation, and CBB-associated inorganic-carbon assimilation.

## Functional-set strategy

Prefer ranked-set analysis based on the DESeq2 Wald statistic when the question is coordinated pathway/module response rather than enrichment among thresholded DEGs.

Do not force every biological module into a nominal KEGG pathway. Use a documented mixture of authoritative annotation and curated modules where needed.

Default RP modules include:

1. **Donor uptake and utilization**
   - formate utilization, including `HZF03_03710–03730` where annotation supports this assignment;
   - H2 metabolism, including `HZF03_04850–04865` where supported;
   - acetate activation, including `acs/HZF03_01070` where supported.
2. **Energy and reducing-power conservation**
   - `nuo` / NADH dehydrogenase;
   - `pet/bc1`;
   - `cco/cox/cyd` terminal oxidase modules as biologically applicable;
   - ATP synthase;
   - `pntAB` and other justified cofactor-balancing functions.
3. **CBB-associated inorganic-carbon assimilation**
   - Form I: `cbbL/HZF03_07635`, `cbbS/HZF03_07640`, `cbbX` where supported;
   - Form II: `cbbM/HZF03_23330` where supported;
   - `prk/cbbP/HZF03_23345` where supported;
   - justified RuBP-regeneration genes such as `fba`, `fbp`, and `tkt`.

Before finalizing a module, verify mechanism-critical gene assignments using authoritative databases and, where needed, literature or sequence-level evidence.

## Fig. 3.5a

Create a compact ranked-enrichment/module plot containing only mechanism-relevant pathways/modules, typically 8–12 rows.

Preferred encoding:

- x-axis: normalized enrichment score or equivalent signed enrichment statistic;
- color: FDR;
- size: core-enrichment gene count or another clearly defined support metric;
- positive/negative direction explicitly tied to coculture versus RP-only.

The full enrichment landscape belongs in Fig. S21.

## Fig. 3.5b

Create the RP selected-gene heatmap with all biological replicates shown individually.

Default display:

- DESeq2 VST values;
- gene-wise Z-score for sample-to-sample pattern;
- adjacent `log2FC` and adjusted P-value/FDR columns.

Group rows by donor utilization, energy/redox conservation, and CBB-associated modules.

Row Z-score represents relative variation across samples for each gene and must not be described as absolute or cross-gene “high expression.”

## Outputs

- curated `RP_modules.tsv` with annotation/evidence source;
- ranked GSEA/module results;
- Fig. 3.5a;
- Fig. 3.5b;
- Fig. S21 complete enrichment;
- Fig. S22 expanded RP module heatmap;
- RP module evidence table.

## Gate 4

`PASS` only when:

- every highlighted module has auditable gene membership;
- GSEA ranking direction is verified;
- main-text pathways are mechanism-relevant rather than cherry-picked after the fact;
- key gene annotations are supported;
- heatmap Z-scores are interpreted correctly;
- claims describe coordinated transcriptional response rather than flux.

---

# Stage 5 — Bath donor-side transcriptional support

## Goal

Determine whether Bath functions required by the donor-side model are transcriptionally represented during cocultivation without fabricating a differential-expression comparison that does not exist.

## Default Bath modules

- methane oxidation: `pmoCAB` and/or `mmoXYBZDC` as encoded and detected;
- methanol oxidation: `mxa` / `xox` systems;
- RuMP-cycle functions such as `hps-phi/hxl` where supported;
- H4MPT-linked C1 oxidation such as `fae–mtd–mch–fhc` or strain-appropriate homologs;
- formate metabolism;
- respiratory electron transport;
- candidate H2-related routes;
- riboflavin biosynthesis/export or other redox-mediator-related functions where genomic/annotation support exists;
- intrinsic Bath CBB cycle.

## Metrics

For each module compute at least:

1. **transcriptional coverage** = stably detected core genes / encoded core genes;
2. **within-Bath expression rank**, preferably median TPM percentile of module core genes within the Bath transcriptome;
3. **replicate consistency**, including detection across replicates and a variation metric when informative.

Define “stably detected” before interpreting the results. The threshold must be data- and pipeline-aware rather than chosen after viewing the preferred result.

## Fig. 3.5c

Create a Bath module support matrix or bubble matrix:

- rows: Bath functional modules;
- columns: Bath signal from each coculture biological replicate;
- size: module coverage or another explicitly defined support metric;
- color: within-Bath expression percentile or rank;
- side annotation: mechanism-critical genes.

Allowed wording: Bath maintained/demonstrated coordinated transcriptional representation of methane oxidation, C1 metabolism, respiratory energy conservation, and candidate donor-related functions during cocultivation.

Disallowed without a Bath comparator: `induced`, `upregulated`, `enhanced by cocultivation`, or equivalent comparative wording.

## Outputs

- curated `Bath_modules.tsv`;
- Bath raw-count/TPM/percentile/consistency table;
- Fig. 3.5c;
- Fig. S23 Bath gene-level TPM/module-coverage support.

## Gate 5

`PASS` only when:

- module definitions are documented before final interpretation;
- coverage and expression-rank formulas are explicit;
- replicate consistency is shown rather than hidden by a median;
- Bath results remain within-species descriptive/supportive evidence;
- cross-species TPM comparisons are not used to imply stronger/weaker expression.

---

# Stage 6 — Cross-species homology and ambiguity audit

## Goal

Audit the mechanism-critical genes highlighted in Stages 4–5 to make sure species attribution is defensible.

## Priority targets

- CBB genes, especially `cbbL/cbbS` and related homologs;
- respiratory-chain homologs used in the main figure;
- formate/H2-related genes;
- any gene with unexpectedly high ambiguous or multimapped support;
- any locus whose attribution materially affects Fig. 3.5d.

## Actions

Use sequence comparison and alignment/read evidence as needed to classify each critical locus as:

- species-unique signal;
- resolvable homologous signal;
- ambiguous signal requiring exclusion, aggregation, or downgraded interpretation.

Do not silently assign ambiguous reads to the preferred organism.

## Outputs

- Fig. S24 conserved-gene/ambiguous-mapping audit;
- locus-level ambiguity/homology table;
- list of Stage 4/5 conclusions that remain valid, require downgrade, or require rerun.

## Gate 6

`PASS` only when every mechanism-critical ambiguous locus is explicitly resolved, excluded, aggregated, or downgraded.

If Stage 6 changes species attribution or removes key genes, mark the affected Stage 4 and/or Stage 5 outputs `REOPENED`, regenerate them, and re-pass their gates before Stage 7.

---

# Stage 7 — Cross-omics integration and mechanistic model

## Goal

Integrate species-resolved transcriptomics with independent gas, metabolite, physiology, perturbation, and isotope evidence into the final mechanistic interpretation.

## Fig. 3.5d conceptual chain

`CH4 → Bath methane oxidation → C1/redox metabolism → candidate formate + H2 + acetate + extracellular redox products → RP uptake/oxidation → respiratory energy conservation → ATP + NADH/NADPH balance → RP CBB-associated response → dark inorganic-carbon incorporation at the community level`

Use different transcriptomic encodings for the two species:

- **Bath**: within-species expression rank, module coverage, and detection consistency;
- **RP**: coculture-versus-RP-only `log2FC`, Wald/FDR, and coordinated module enrichment.

Never use one shared TPM color scale to imply direct cross-species expression comparability.

## Evidence-edge classes

Each connection in Fig. 3.5d or the evidence matrix must be marked as one of:

- **Directly observed / independently supported** — e.g. measured gas/metabolite/physiology/isotope pattern directly relevant to the edge;
- **Multi-evidence interpretation** — supported by converging but non-flux-resolved data;
- **Candidate / transcriptionally plausible** — gene/transcript support without direct transfer proof;
- **Unresolved** — retained only when useful to show the remaining boundary.

Use stronger/solid visual links only for better-supported connections and dashed/candidate links for unresolved transfer routes.

Acetate may connect to RP `acs → acetyl-CoA` when supported by RP substrate-use data, but do not draw a complete Bath acetate-production pathway unless Bath genomic/transcriptional evidence supports it.

## Required evidence boundaries

1. **Species-specific isotope incorporation**
   - bulk community EA–IRMS does not establish that 13C entered RP biomass;
   - RP CBB transcription plus community-level 13C incorporation may be described as mutually consistent evidence, not direct species-resolved isotope proof.
2. **Bath induction**
   - no Bath-only RNA-seq comparator means no claim that Bath pathways were induced/upregulated by cocultivation.
3. **Metabolic flux**
   - transcripts do not prove donor-to-recipient flux or quantify the contribution of formate, H2, acetate, riboflavin-like mediators, or any other route.
4. **Community ATP/NAD(H)**
   - mixed-culture ATP/NAD(H) measurements remain community-level unless species-resolved evidence exists.
5. **Multiple evidence lines**
   - mechanistic interpretation may be strengthened by converging independent evidence; do not require a single assay to prove the entire model, but do not erase the unresolved step between evidence layers.

## Outputs

- Fig. 3.5d;
- cross-evidence matrix linking each model edge to data sources;
- claim-strength table for Results/Discussion drafting;
- explicit unresolved questions.

## Gate 7

`PASS` only when:

- every major arrow has an evidence class;
- transcriptomic evidence is not described as flux proof;
- community-level 13C is not attributed specifically to RP;
- Bath expression is not described as induced without a comparator;
- community ATP/NAD(H) is not silently assigned to RP;
- stronger mechanistic wording is supported by multiple relevant evidence lines rather than one isolated assay.

When manuscript claims are drafted from these outputs, also apply `PR-CAL` evidence calibration.

---

# Stage 8 — Final package and manuscript handoff

## Goal

Produce the reproducible, publication-ready analysis package and freeze what was actually validated.

## Required deliverables

Unless the task is explicitly narrower, prepare:

- **Fig. 3.5a** — RP pathway/module ranked enrichment;
- **Fig. 3.5b** — RP selected-gene VST Z-score heatmap with log2FC/FDR;
- **Fig. 3.5c** — Bath transcriptional support matrix;
- **Fig. 3.5d** — species-resolved integrated evidence model;
- **Fig. S18** — sequencing/species-assignment QC;
- **Fig. S19** — RP PCA/correlation/clustering;
- **Fig. S20** — RP volcano/MA;
- **Fig. S21** — complete enrichment background;
- **Fig. S22** — expanded RP functional-module heatmap;
- **Fig. S23** — Bath gene-level TPM/module-coverage support;
- **Fig. S24** — conserved-gene/ambiguous-mapping audit;
- RP full DESeq2 table;
- Bath raw-count/TPM/percentile/consistency table;
- pathway/module evidence table with annotation source and evidence level;
- cross-evidence model table;
- software/environment/parameter manifest;
- source tables and scripts for every main figure panel;
- concise analysis README explaining what was run, what passed, and what remains unresolved;
- final stage ledger with commit/version references.

Do not perform WGCNA by default for the six-sample RP comparison. Reconsider only if a substantially larger and appropriately structured sample set becomes available.

## Gate 8

`PASS` only when:

- all main panels trace back to machine-readable source tables and scripts;
- all stage gates and exceptions are visible;
- software versions and key parameters are recorded;
- reference versions and sample design are frozen in the manifest;
- any reopened stage has been revalidated;
- known limitations are retained rather than polished away;
- the final figures and tables correspond to the same validated analysis version.

Do not auto-merge a meaningful workflow execution or analysis-method change without explicit user approval.

# Change-control matrix

Use this minimum dependency logic when upstream decisions change:

| Change | Reopen at least |
| --- | --- |
| sample identity / replicate / contrast / batch design | Stage 0, then Stages 3–8 as affected; Stage 2 if sample set changes |
| reference genome/annotation or species-prefix scheme | Stages 1–8 |
| mapper / species-assignment rule | Stages 2–8 |
| count-generation rule | Stages 3–8 |
| RP module membership / annotation | Stages 4, 6, 7, 8 |
| Bath module membership or stable-detection threshold | Stages 5, 6, 7, 8 |
| homology audit changes species attribution | affected Stage 4/5 plus Stages 6–8 |
| independent metabolite/isotope/physiology evidence changes | Stages 7–8 |
| figure-only aesthetic edit with unchanged source data | Stage 8 visual QA only |

# Positive case

Input request: `Run WF-RNA-DUAL on the Bath–RP coculture RNA-seq and prepare Fig. 3.5 plus S18–S24.`

Expected behavior: start at Stage 0, present the frozen sample/reference/contrast contract, stop for checkpoint, and proceed one stage at a time only after each gate passes.

# Negative control

Input request: `Rewrite this paragraph about cbbL expression for the Discussion.`

Expected behavior: do not launch the RNA-seq workflow merely because a transcriptomic gene is mentioned. Route as manuscript/scientific-claim review unless transcriptomic re-analysis is explicitly requested.

# Maturity

Status: **experimental / specification-complete, stage-gated, not yet forward-validated on the user’s actual FASTQ dataset**.

Promote to `stable / forward-validated once` only after one complete real-data run verifies the stage-control behavior, species assignment, RP differential analysis, Bath support metrics, ambiguity audit, figure-source traceability, and evidence boundaries.
