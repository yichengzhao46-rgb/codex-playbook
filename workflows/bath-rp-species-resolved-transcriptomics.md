# Bath–RP Species-Resolved Transcriptomics Workflow

Use this workflow for transcriptomic analysis of the defined *Methylococcus capsulatus* Bath–*Rhodopseudomonas palustris* coculture when the goal is to connect Bath donor-side metabolism with RP recipient-side energy/redox responses and CBB-associated dark inorganic-carbon assimilation without exceeding the evidence supported by bulk RNA-seq and community-level isotope measurements.

This is a reusable analysis method. Project-specific FASTQ files, reference genomes, count matrices, figures, and outputs belong in the relevant execution/project repository, not in `codex-playbook`.

## Workflow key and invocation

Canonical workflow key: `WF-RNA-DUAL`

Treat any of the following as an explicit request to use this workflow:

- `run WF-RNA-DUAL`
- `run the Bath–RP transcriptomics workflow`
- `run the Bath–RP RNA-seq full workflow`
- `run the Fig. 3.5 / S18–S24 transcriptomics workflow`
- a request for species-resolved Bath–RP coculture transcriptomics that includes differential expression, pathway/module analysis, or integrated mechanistic interpretation

Do not trigger this workflow for single-gene RT-qPCR, ordinary single-species RNA-seq, metagenomics, or manuscript wording review that does not require transcriptomic analysis.

## Primary objective

Produce a reproducible, species-resolved analysis that supports the following evidence chain:

`Bath methane oxidation and donor-side metabolic capacity → candidate diffusible products / reducing equivalents → RP donor utilization and respiratory energy conservation → RP CBB-associated transcriptional response → consistency with enhanced community-level inorganic-carbon incorporation`

The workflow must support this chain without claiming that transcriptomics alone proves metabolite flux, species-specific isotope incorporation, or induction of Bath pathways in the absence of a Bath-only transcriptomic comparator.

## Default execution route

This is normally a `PR-DATA` task with scientific interpretation constraints.

- **Codex**: primary executor for repository-native pipeline construction, combined-reference preparation, mapping, quantification, DESeq2/GSEA scripts, figure generation, reproducibility, and validation.
- **ChatGPT**: framing, pathway/module curation, literature/database interpretation, evidence-boundary review, and final figure/manuscript reasoning.
- **GitHub**: versioned source of truth for scripts, parameters, manifests, analysis notes, validation evidence, and PR review.
- **Optional ChatGPT plugins**: NGS Analysis Workbench, Biological Sequence & Alignment Viewer, Life Sciences Databases, and Life Sciences Literature may be used for cross-checking or specialist inspection when available. They are not required for completion and must not become hidden dependencies.

Use one primary writer at a time. If Codex is executing the analysis, ChatGPT should review requirements/results rather than editing the same active files concurrently.

## Required inputs

Before analysis, resolve or explicitly mark missing:

1. raw or cleaned FASTQ files for every biological replicate;
2. sample metadata with condition, replicate, library layout, strandedness if known, sequencing batch if applicable, and any other design factor that could affect the model;
3. authoritative Bath reference genome and annotation;
4. authoritative RP reference genome and annotation;
5. expected sample groups, including the RP-only versus coculture comparison used for RP differential expression;
6. confirmation that Bath lacks an equivalent Bath-only RNA-seq comparator unless new data are supplied;
7. the target output scope: Fig. 3.5a–d, Figs. S18–S24, tables, or a subset.

Do not infer missing sample identities or biological replicates from filenames alone when the mapping is ambiguous.

## Phase 1 — Reference preparation and provenance

Build a combined Bath + RP reference for competitive species assignment.

Requirements:

- concatenate the two authoritative genomes and compatible annotations;
- add unambiguous species prefixes to sequence, gene, transcript, and feature identifiers where needed;
- preserve an ID mapping table back to the original annotation;
- record accessions, versions, download dates, checksums when practical, and any annotation transformations;
- generate an auditable manifest of the exact combined reference used.

Preferred principle: competitive assignment against the combined reference rather than sequentially mapping first to one species and then the other. Sequential approaches can bias assignment toward the first reference when homologous reads cross-map.

## Phase 2 — Sequencing and species-assignment QC

For each sample, record at minimum:

`raw reads → post-filter reads → non-rRNA reads → mapped reads → Bath uniquely assigned → RP uniquely assigned → ambiguous/multimapped → unmapped → gene-assigned reads`

Also inspect when available:

- base-quality and adapter metrics;
- read length and library layout;
- duplication or library-complexity signals;
- inferred/expected strandedness;
- rRNA fraction;
- mapping rate;
- species-assignment proportions;
- unexpected contamination or extreme sample imbalance;
- replicate consistency.

The exact mapper/quantifier may be selected according to the execution environment, but the choice and parameters must be recorded. Do not silently change aligner or quantification strategy between samples.

Expected primary output: **Fig. S18** and a machine-readable QC table.

## Phase 3 — Species-resolved quantification

Generate species-resolved gene-level count matrices and expression summaries.

### RP

Retain raw integer counts for DESeq2. TPM may be generated for descriptive abundance checks but must not be used as DESeq2 input.

### Bath

Generate raw counts and TPM or another explicitly documented within-sample abundance metric. Bath expression is descriptive/supportive unless a valid Bath comparison is supplied.

Maintain:

- original counts;
- filtered counts used for downstream analysis;
- species assignment summary;
- gene ID/annotation mapping;
- software versions and parameters.

## Phase 4 — RP comparative transcriptomics

Default comparison: `coculture-derived RP signal vs RP-only`, using the user-approved biological design.

Use DESeq2 or an equivalently justified count-based model. The default outputs should include:

- `baseMean`;
- `log2FoldChange`;
- `lfcSE`;
- Wald statistic;
- raw P value;
- BH-adjusted P value/FDR.

Use transformed counts such as VST for PCA, correlation, clustering, and the selected-gene heatmap. Do not use VST or TPM as the count input for DESeq2 inference.

Expected supporting outputs:

- **Fig. S19**: RP PCA, sample correlation, and hierarchical clustering;
- **Fig. S20**: RP volcano and MA plots;
- full DESeq2 results table.

## Phase 5 — RP pathway and curated-module analysis

Prefer ranked-set analysis based on the DESeq2 Wald statistic when the objective is coordinated pathway/module response rather than enrichment among a thresholded DEG subset.

Do not force every biological module into a nominal KEGG pathway. Use a documented mixture of authoritative annotation and curated modules when needed.

Default mechanism-oriented RP modules include:

1. **Donor uptake and utilization**
   - formate utilization, including `HZF03_03710–03730` where annotation supports this assignment;
   - H2 metabolism, including `HZF03_04850–04865` where annotation supports this assignment;
   - acetate activation, including `acs/HZF03_01070` where annotation supports this assignment.
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

Before finalizing a module, verify gene annotation through authoritative databases and, for mechanism-critical assignments, literature or sequence-level evidence.

### Fig. 3.5a

Create a compact enrichment/module plot containing only mechanism-relevant pathways/modules, typically 8–12 rows.

Preferred encoding:

- x-axis: normalized enrichment score or equivalent signed enrichment statistic;
- color: FDR;
- size: core-enrichment gene count or another clearly defined support metric;
- positive/negative direction: explicitly tied to coculture versus RP-only.

The full enrichment landscape belongs in **Fig. S21**.

### Fig. 3.5b

Create the RP selected-gene heatmap with all biological replicates shown individually.

Default expression display:

- DESeq2 VST values;
- gene-wise Z-score for sample-to-sample pattern;
- adjacent `log2FC` and adjusted P-value/FDR columns.

Group rows by donor utilization, energy/redox conservation, and CBB-associated modules.

Interpretation boundary: row Z-score represents relative variation across samples for each gene and must not be described as absolute or cross-gene “high expression.” Use TPM or count-based abundance summaries separately when abundance ranking matters.

The larger module/gene heatmap belongs in **Fig. S22**.

## Phase 6 — Bath within-species transcriptional support

If there is no Bath-only transcriptomic comparator, do **not** run or present Bath coculture-versus-monoculture differential-expression claims.

Instead quantify whether Bath functions required by the proposed donor-side model are transcriptionally represented during cocultivation.

Default Bath modules:

- methane oxidation: `pmoCAB` and/or `mmoXYBZDC` as encoded and detected;
- methanol oxidation: `mxa` / `xox` systems;
- RuMP-cycle functions such as `hps-phi/hxl` where annotation supports them;
- H4MPT-linked C1 oxidation: `fae–mtd–mch–fhc` or strain-appropriate homologs;
- formate metabolism;
- respiratory electron transport;
- candidate H2-related routes;
- riboflavin biosynthesis/export or other redox-mediator-related functions where genomic/annotation support exists;
- intrinsic Bath CBB cycle.

For each module, compute and retain at least:

1. **transcriptional coverage** = stably detected core genes / encoded core genes;
2. **within-Bath expression rank**, preferably median TPM percentile of the module core genes within the Bath transcriptome;
3. **replicate consistency**, including detection across replicates and a variation metric when informative.

Define “stably detected” explicitly before analysis. A default may be detection in all biological replicates above a documented minimal expression threshold, but the threshold must be data- and pipeline-aware rather than invented after viewing the desired result.

### Fig. 3.5c

Create a Bath module support matrix or bubble matrix:

- rows: Bath functional modules;
- columns: Bath signal from each coculture biological replicate;
- size: module coverage or another explicitly defined coverage measure;
- color: within-Bath expression percentile or rank;
- side annotation: mechanism-critical genes.

Allowed conclusion: Bath maintained/demonstrated coordinated transcriptional representation of methane oxidation, C1 metabolism, respiratory energy conservation, and candidate donor-related functions during cocultivation.

Disallowed without a Bath comparator: `induced`, `upregulated`, `enhanced by cocultivation`, or equivalent comparative wording.

Supporting gene-level Bath heatmaps, TPM tables, coverage summaries, and replicate consistency belong in **Fig. S23** and the Bath expression supplementary table.

## Phase 7 — Cross-species homology and ambiguous-mapping audit

Mechanism-critical genes that have homologs in both organisms require explicit species-assignment review.

Prioritize:

- CBB genes, especially `cbbL/cbbS` and related homologs;
- respiratory-chain homologs used in the main figure;
- formate/H2-related genes;
- any gene with unexpectedly high ambiguous or multimapped read support;
- any locus whose interpretation materially affects Fig. 3.5d.

Use sequence comparison and alignment/read evidence as needed to distinguish:

- species-unique signal;
- resolvable homologous signal;
- ambiguous signal that should be excluded or downgraded.

Do not silently assign ambiguous reads to a preferred organism.

Expected primary output: **Fig. S24** plus an ambiguity/homology audit table.

## Phase 8 — Integrated mechanistic model

### Fig. 3.5d

Integrate transcriptomics with independent physiological/metabolic/isotope evidence. The conceptual chain is:

`CH4 → Bath methane oxidation → C1/redox metabolism → candidate formate + H2 + acetate + extracellular redox products → RP uptake/oxidation → respiratory energy conservation → ATP + NADH/NADPH balance → RP CBB-associated response → dark inorganic-carbon incorporation at the community level`

Use different transcriptomic encodings for the two species:

- **Bath**: within-species expression rank, module coverage, and detection consistency;
- **RP**: coculture-versus-RP-only `log2FC`, Wald/FDR, and coordinated module enrichment.

Never use one shared TPM color scale to imply direct cross-species expression comparability.

Use evidence-aware edges:

- solid or otherwise stronger links only where independent metabolite, gas, physiological, or isotope evidence supports the connection;
- dashed/candidate links where support is genomic/transcriptional but direct transfer remains unresolved.

Acetate may connect to RP `acs → acetyl-CoA` when supported by RP substrate-use data, but do not draw a complete Bath acetate-production pathway unless the Bath genomic/transcriptional evidence supports it.

## Phase 9 — Required evidence boundaries

The workflow must enforce all of the following:

1. **Species-specific isotope incorporation**
   - bulk community EA–IRMS does not establish that 13C entered RP biomass;
   - RP CBB transcription plus community-level 13C incorporation may be described as mutually consistent evidence, not direct species-resolved isotope proof.
2. **Bath induction**
   - no Bath-only RNA-seq comparator means no claim that Bath pathways were induced/upregulated by cocultivation.
3. **Metabolic flux**
   - transcripts do not prove donor-to-recipient flux or quantify the contribution of formate, H2, acetate, riboflavin-like mediators, or any other candidate route.
4. **Community ATP/NAD(H)**
   - mixed-culture ATP/NAD(H) measurements are community-level unless species-resolved evidence exists.
5. **Multiple evidence lines**
   - mechanistic interpretation should integrate transcription with metabolite, gas, physiology, perturbation, and isotope evidence where available rather than requiring every individual assay to prove the mechanism alone.

When manuscript claims are drafted from these outputs, also apply the repository’s evidence-calibration workflow.

## Phase 10 — Deliverables

Unless the task is explicitly narrower, generate or prepare the data objects required for:

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
- software/environment/parameter manifest;
- a concise analysis README explaining what was run and what remains unresolved.

Do not perform WGCNA by default for the six-sample RP comparison. Reconsider only if a substantially larger and appropriately structured sample set becomes available.

## Validation gates

Before calling the workflow complete, check:

- combined-reference IDs are species-unambiguous and traceable to source annotations;
- species-assignment QC is reported and ambiguous reads are quantified;
- sample design and replicate labels are verified;
- DESeq2 receives unnormalized integer counts;
- VST/Z-score is limited to visualization/structure, not DE inference;
- GSEA/module direction is tied to an explicit contrast;
- curated modules have auditable gene membership and annotation support;
- Bath results are descriptive/supportive unless a valid comparator exists;
- main-figure claims stay within species and assay evidence boundaries;
- all main panels can be traced back to machine-readable source tables and scripts;
- software versions, key parameters, and the analysis head commit are recorded;
- failed or blocked checks remain visible.

## Positive case

Input request: `Run WF-RNA-DUAL on the Bath–RP coculture RNA-seq and prepare Fig. 3.5 plus S18–S24.`

Expected behavior: inspect sample/reference inputs, prepare the combined-reference and species-assignment plan, execute or stage the reproducible analysis, separate RP comparative inference from Bath descriptive support, generate required tables/figures, and flag unresolved evidence boundaries.

## Negative control

Input request: `Rewrite this paragraph about cbbL expression for the Discussion.`

Expected behavior: do not launch the full RNA-seq workflow merely because a transcriptomic gene is mentioned. Route as manuscript/scientific-claim review unless the user explicitly requests transcriptomic re-analysis.

## Maturity

Status: **experimental / specification-complete, not yet forward-validated on the user’s actual FASTQ dataset**.

Promote to `stable / forward-validated once` only after one complete real-data run verifies species assignment, RP differential analysis, Bath support metrics, figure-source traceability, and the stated evidence boundaries.
