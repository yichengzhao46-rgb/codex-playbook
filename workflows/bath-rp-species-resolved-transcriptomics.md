# Bath–RP Species-Resolved Transcriptomics Workflow

Use this workflow for transcriptomic analysis of the defined *Methylococcus capsulatus* Bath–*Rhodopseudomonas palustris* coculture when the goal is to connect Bath donor-side metabolism with RP recipient-side energy/redox responses and CBB-associated dark inorganic-carbon assimilation without exceeding the evidence supported by bulk RNA-seq and community-level isotope measurements.

Project-specific FASTQ files, references, count matrices, figures, and results belong in the execution/project repository, not in `codex-playbook`.

## Workflow key and invocation

Canonical workflow key: `WF-RNA-DUAL`

Trigger on:

- `run WF-RNA-DUAL`
- `run the Bath–RP transcriptomics workflow`
- `run the Bath–RP RNA-seq full workflow`
- `run the Fig. 3.5 / S18–S24 transcriptomics workflow`
- species-resolved Bath–RP coculture transcriptomics involving differential expression, pathway/module analysis, or mechanistic integration

Do not trigger for single-gene RT-qPCR, ordinary single-species RNA-seq, metagenomics, or wording-only manuscript review.

## Primary objective

Support the evidence chain:

`Bath methane oxidation and donor-side metabolic capacity → candidate diffusible products / reducing equivalents → RP donor utilization and respiratory energy conservation → RP CBB-associated transcriptional response → consistency with enhanced community-level inorganic-carbon incorporation`

Transcriptomics must not be used alone to prove metabolite flux, species-specific isotope incorporation, or Bath pathway induction without a valid Bath comparator.

## Default execution route

This is normally a `PR-DATA` task with scientific-interpretation constraints.

- **Codex**: primary executor for combined-reference preparation, mapping, quantification, DESeq2/GSEA, pathway/module tables, plotting, provenance, and reproducible validation.
- **ChatGPT**: scientific framing, module curation decisions, evidence-boundary review, literature synthesis, and final interpretation.
- **GitHub**: source of truth for scripts, parameters, manifests, gene-set versions, validation records, and PR review.

### Required plugin stack

A standard `WF-RNA-DUAL` run should use **all four** of the following specialist plugins when they are accessible in the active environment. They are complementary checkpoints, not interchangeable alternatives.

1. **NGS Analysis Workbench — required sequencing-analysis checkpoint**
   - inspect FASTQ/QC outputs and standard bulk RNA-seq analysis artifacts;
   - cross-check read QC, quantification/count outputs, and standard differential-expression/QC results where supported;
   - compare its outputs with the repository-native Codex pipeline rather than allowing the plugin to silently define the custom dual-species mapping logic.

2. **Biological Sequence & Alignment Viewer — required sequence/species-assignment checkpoint**
   - inspect Bath/RP homologs, conserved loci, ambiguous mappings, and mechanism-critical sequence assignments;
   - prioritize CBB genes, formate/H2 genes, respiratory-chain homologs, and any locus that materially affects Fig. 3.5;
   - use mapped-read/alignment evidence when available to verify that species-specific interpretation is defensible.

3. **Life Sciences Databases — required pathway/function-validation checkpoint**
   - run [`WF-PATHWAY-VALIDATE`](pathway-module-database-validation.md) before freezing RP or Bath curated gene sets;
   - verify the chain `exact gene/locus → molecular function/reaction → pathway/module role` using organism-specific evidence where possible;
   - use appropriate database resources such as UniProt, QuickGO, Rhea, STRING, Reactome when relevant, together with KEGG/eggNOG/MetaCyc or equivalent resources available in the execution environment;
   - do not treat one pathway label or enrichment result as sufficient proof of mechanism.

4. **Life Sciences Literature — required literature/evidence checkpoint**
   - validate mechanism-critical, strain-specific, unusual, conflicting, or high-impact pathway assignments against primary literature;
   - support interpretation of RP donor use, respiratory/redox response, CBB-associated transcription, Bath donor-side pathways, and evidence boundaries;
   - use literature to calibrate what can be claimed from transcription versus metabolite, physiological, perturbation, and isotope evidence.

**Rosalind Workbench is explicitly excluded from this workflow.**

If one of the four required plugins is temporarily unavailable, do not silently omit its role. Record the checkpoint as `BLOCKED`, use a documented repository/database/literature fallback where possible, and state that the plugin-specific cross-check remains unperformed. A plugin failure must not be converted into a pass.

Use one primary writer at a time.

## Required inputs

Resolve or explicitly mark missing:

1. FASTQ files for every biological replicate;
2. sample metadata: condition, replicate, library layout, strandedness if known, batch if applicable;
3. authoritative Bath genome + annotation;
4. authoritative RP genome + annotation;
5. RP-only versus coculture design for RP differential expression;
6. whether a Bath-only RNA-seq comparator exists;
7. requested output scope: Fig. 3.5a–d, S18–S24, tables, or subset.

Do not infer ambiguous sample identities from filenames alone.

## Phase 1 — Reference preparation and provenance

Build a combined Bath + RP reference for competitive species assignment.

Requirements:

- concatenate authoritative genomes and compatible annotations;
- add species-unambiguous prefixes to sequence/gene/transcript/feature identifiers as needed;
- preserve an ID mapping table to original annotations;
- record accessions, versions, dates, checksums when practical, and annotation transformations;
- generate a manifest for the exact combined reference.

Prefer competitive assignment against the combined reference. Do not use sequential Bath-first/RP-second mapping as the default because homologous reads can be biased toward the first reference.

## Phase 2 — Sequencing and species-assignment QC

For each sample report at minimum:

`raw reads → post-filter reads → non-rRNA reads → mapped reads → Bath unique → RP unique → ambiguous/multimapped → unmapped → gene-assigned`

Inspect:

- base quality/adapters;
- read length/layout;
- duplication/library complexity;
- strandedness;
- rRNA fraction;
- mapping rate;
- Bath/RP assignment proportions;
- contamination/extreme imbalance;
- replicate consistency.

Record mapper/quantifier, version, and parameters. Do not silently change strategies across samples.

### Plugin checkpoint A — NGS Analysis Workbench

Run the NGS plugin on the standard QC/quantification scope it supports and compare its QC/count/DE artifacts with the Codex pipeline. Record agreements, discrepancies, and unsupported custom steps. The custom Bath/RP competitive-assignment policy remains controlled by the repository workflow.

Primary output: **Fig. S18** + machine-readable QC table + plugin cross-check note.

## Phase 3 — Species-resolved quantification

Generate species-resolved gene-level counts and expression summaries.

### RP

Retain raw integer counts for DESeq2. TPM may be generated for descriptive abundance checks but not used as DESeq2 input.

### Bath

Generate raw counts and TPM or another documented within-sample abundance metric. Bath expression remains descriptive/supportive unless a valid comparator is supplied.

Retain original counts, filtered counts, assignment summary, ID/annotation mapping, and software/parameter provenance.

## Phase 4 — RP comparative transcriptomics

Default contrast: `coculture-derived RP signal vs RP-only` using the verified biological design.

Use DESeq2 or an equivalently justified count-based model. Output:

- `baseMean`;
- `log2FoldChange`;
- `lfcSE`;
- Wald statistic;
- P value;
- BH-adjusted P/FDR.

Use VST or another justified transform for PCA/correlation/clustering/heatmaps, not for DE inference.

Outputs:

- **Fig. S19**: PCA, sample correlation, clustering;
- **Fig. S20**: volcano + MA;
- full RP DESeq2 table.

Use NGS Analysis Workbench as an independent standard-analysis cross-check where its supported workflow overlaps this phase.

## Phase 5 — Mandatory pathway/function validation before RP enrichment

Before GSEA, selected-gene heatmaps, or mechanistic interpretation, run [`WF-PATHWAY-VALIDATE`](pathway-module-database-validation.md).

For every mechanism-critical RP module, verify:

`exact RP gene/locus → molecular function/reaction → pathway/module role`

### Plugin checkpoint B — Life Sciences Databases

Use organism-specific evidence first. Prioritize:

- **UniProt** for protein identity/function, EC numbers, domains, and cross-references;
- **QuickGO** for GO molecular-function and biological-process annotations;
- **Rhea** for biochemical reaction identity when a reaction assignment matters;
- **STRING** for enrichment/functional-association/context support, not as sole biochemical proof;
- **Reactome** only when a relevant organism/event mapping exists; do not directly transfer human pathway definitions to bacterial genes.

Also use KEGG/eggNOG/MetaCyc or equivalent resources when available in the execution environment.

### Plugin checkpoint C — Life Sciences Literature

For mechanism-critical, conflicting, unusual, or strain-specific assignments, verify with primary literature before freezing the module. Literature support is especially important where database annotation alone does not distinguish a complete physiological route from a plausible homologous function.

Freeze a versioned RP gene-set file after validation. Do not adjust membership merely to improve enrichment direction.

### Default RP modules to validate

**Donor uptake/utilization**
- proposed formate module including `HZF03_03710–03730` where supported;
- proposed H2 module including `HZF03_04850–04865` where supported;
- acetate activation including `acs/HZF03_01070` where supported.

**Energy/reducing-power conservation**
- `nuo`;
- `pet/bc1`;
- `cco/cox/cyd` as biologically applicable;
- ATP synthase;
- `pntAB` and justified cofactor-balancing functions.

**CBB-associated inorganic-carbon assimilation**
- Form I: `cbbL/HZF03_07635`, `cbbS/HZF03_07640`, `cbbX` where supported;
- Form II: `cbbM/HZF03_23330` where supported;
- `prk/cbbP/HZF03_23345` where supported;
- justified RuBP-regeneration genes such as `fba`, `fbp`, `tkt`.

Classify validated genes as core, provisional/extended, excluded, or unresolved. Main-text modules should be driven by well-supported core genes.

## Phase 6 — RP ranked pathway/module analysis

Prefer ranked-set analysis using the DESeq2 Wald statistic when the goal is coordinated pathway/module response rather than enrichment among a thresholded DEG list.

Do not force every curated biological module into a nominal KEGG pathway.

### Fig. 3.5a

Show only mechanism-relevant modules, typically 8–12 rows.

Preferred encoding:

- x: normalized enrichment score or equivalent signed statistic;
- color: FDR;
- size: core-enrichment gene count or clearly defined support metric;
- direction explicitly tied to coculture versus RP-only.

Full enrichment background belongs in **Fig. S21**.

### Fig. 3.5b

Show all biological replicates individually.

Default:

- VST expression;
- gene-wise Z-score across samples;
- adjacent log2FC and FDR columns;
- rows grouped by donor utilization, energy/redox conservation, CBB-associated modules.

Row Z-score represents relative within-gene sample variation and must not be described as cross-gene absolute “high expression.” Use TPM/count summaries separately when abundance rank matters.

Expanded heatmap belongs in **Fig. S22**.

## Phase 7 — Mandatory Bath module validation and within-species support

If no Bath-only transcriptomic comparator exists, do not present Bath coculture-versus-monoculture differential-expression claims.

Before calculating module coverage, run `WF-PATHWAY-VALIDATE` for Bath modules using **Life Sciences Databases + Life Sciences Literature**.

Default Bath modules to validate:

- methane oxidation: `pmoCAB` and/or `mmoXYBZDC` as encoded;
- methanol oxidation: `mxa/xox`;
- RuMP functions such as `hps-phi/hxl` where supported;
- H4MPT-linked C1 oxidation: `fae–mtd–mch–fhc` or strain-appropriate homologs;
- formate metabolism;
- respiratory electron transport;
- candidate H2-related routes;
- riboflavin biosynthesis/export or redox-mediator-related functions where supported;
- intrinsic Bath CBB cycle.

For candidate H2 and riboflavin/redox-mediator routes, require stronger validation than gene-name similarity alone; retain as candidate/provisional if the biochemical or pathway link is incomplete.

After freezing the validated Bath module definitions, calculate:

1. **transcriptional coverage** = stably detected core genes / encoded core genes;
2. **within-Bath expression rank**, preferably median TPM percentile of core genes;
3. **replicate consistency**, including detection across replicates and a variation metric when useful.

Define “stably detected” before outcome-driven interpretation.

### Fig. 3.5c

Use a Bath module support/bubble matrix:

- rows: validated Bath modules;
- columns: coculture Bath signal for each replicate;
- size: module coverage;
- color: within-Bath expression percentile/rank;
- side labels: validated mechanism-critical genes.

Allowed: Bath maintained/demonstrated transcriptional representation of methane oxidation, C1 metabolism, respiratory energy conservation, and candidate donor-related functions during cocultivation.

Disallowed without comparator: `induced`, `upregulated`, `enhanced by cocultivation`.

Supporting data belong in **Fig. S23** and the Bath expression table.

## Phase 8 — Cross-species homology and ambiguous-mapping audit

Explicitly review mechanism-critical homologs in both organisms, prioritizing:

- `cbbL/cbbS` and related CBB genes;
- respiratory-chain homologs used in main figures;
- formate/H2 genes;
- genes with unexpectedly high ambiguous/multimapped support;
- loci central to Fig. 3.5d.

### Plugin checkpoint D — Biological Sequence & Alignment Viewer

Use the sequence/alignment viewer to inspect the relevant Bath/RP sequences, homolog relationships, alignments, and mapped-read evidence where supported. Classify each audited locus as:

- species-unique;
- resolvable homologous;
- ambiguous/unresolved.

Do not silently assign ambiguous reads to a preferred organism. A mechanism-critical unresolved locus must be downgraded or excluded from species-specific interpretation.

Output: **Fig. S24** + ambiguity/homology table + sequence-viewer audit note.

## Phase 9 — Integrated mechanism model

### Fig. 3.5d

Integrate validated transcriptomic modules with independent physiological/metabolic/isotope evidence:

`CH4 → Bath methane oxidation → C1/redox metabolism → candidate formate + H2 + acetate + extracellular redox products → RP uptake/oxidation → respiratory energy conservation → ATP + NADH/NADPH balance → RP CBB-associated response → dark inorganic-carbon incorporation at the community level`

Use different transcriptomic encodings:

- **Bath**: within-species expression rank, module coverage, detection consistency;
- **RP**: coculture-vs-RP-only log2FC/Wald/FDR + module enrichment.

Do not use one shared TPM scale to imply direct Bath/RP expression comparability.

Use stronger links only where independent metabolite/gas/physiology/isotope evidence supports the connection. Keep genomic/transcriptional-only routes dashed/candidate.

Do not draw a complete Bath acetate-production, H2-production, or mediator pathway unless validated gene/reaction evidence supports it.

Before finalizing Fig. 3.5d, use **Life Sciences Literature** to check that the proposed interpretation is consistent with relevant published physiology and that the wording does not exceed the underlying evidence.

## Phase 10 — Required evidence boundaries

1. **Species-specific isotope incorporation**: bulk community EA–IRMS does not prove 13C entered RP biomass. RP CBB transcription and community-level 13C incorporation may be described as mutually consistent evidence.
2. **Bath induction**: no Bath comparator means no induced/upregulated claims.
3. **Metabolic flux**: transcripts do not prove donor-to-recipient flux or quantify formate/H2/acetate/mediator contributions.
4. **Community ATP/NAD(H)**: mixed-culture ATP/NAD(H) remains community-level unless species-resolved.
5. **Pathway completeness**: expression of partial/candidate pathways must not be presented as a complete confirmed route.
6. **Multiple evidence lines**: integrate transcriptomics with metabolite, gas, physiology, perturbation, and isotope evidence rather than requiring any single assay to prove the mechanism alone.

When manuscript claims are drafted, also apply the repository evidence-calibration workflow.

## Phase 11 — Deliverables

Unless explicitly narrowed, prepare:

- **Fig. 3.5a** — validated RP pathway/module ranked enrichment;
- **Fig. 3.5b** — validated RP selected-gene VST Z-score heatmap with log2FC/FDR;
- **Fig. 3.5c** — validated Bath transcriptional support matrix;
- **Fig. 3.5d** — integrated species-resolved evidence model;
- **S18** — sequencing/species-assignment QC;
- **S19** — RP PCA/correlation/clustering;
- **S20** — volcano/MA;
- **S21** — full enrichment;
- **S22** — expanded RP module heatmap;
- **S23** — Bath TPM/module-coverage support;
- **S24** — homolog/ambiguous-mapping audit;
- RP DESeq2 table;
- Bath raw-count/TPM/percentile/consistency table;
- `pathway_module_validation.tsv` with database-backed evidence classes and include/exclude decisions;
- versioned RP and Bath gene-set files;
- unresolved pathway/annotation conflict list;
- software/environment/parameter manifest;
- concise analysis README;
- **plugin checkpoint report** recording NGS Analysis Workbench, Biological Sequence & Alignment Viewer, Life Sciences Databases, and Life Sciences Literature as `PASS`, `PARTIAL`, or `BLOCKED`, with what each actually checked.

Do not perform WGCNA by default for the six-sample RP comparison. Reconsider only with a substantially larger, suitable sample set.

## Validation gates

Before completion verify:

- combined-reference IDs are species-unambiguous and traceable;
- ambiguous reads are quantified;
- sample design/replicates are verified;
- DESeq2 receives raw integer counts;
- VST/Z-score is visualization only;
- GSEA direction maps to an explicit contrast;
- NGS Analysis Workbench checkpoint is completed or explicitly `BLOCKED`;
- Biological Sequence & Alignment Viewer checkpoint is completed or explicitly `BLOCKED`;
- Life Sciences Databases validation is completed or explicitly `BLOCKED`;
- Life Sciences Literature validation is completed or explicitly `BLOCKED`;
- gene-set membership is frozen and auditable before final enrichment/figure generation;
- provisional genes are separated from core genes;
- pathway/reaction conflicts remain visible;
- Bath results are descriptive/supportive without comparator;
- main claims stay within assay/species evidence boundaries;
- all main panels trace to machine-readable source tables/scripts;
- software versions, parameters, database access date/version when available, plugin checkpoint status, and analysis commit are recorded;
- failed/blocked checks remain explicit.

## Positive case

Input: `Run WF-RNA-DUAL on the Bath–RP coculture RNA-seq and prepare Fig. 3.5 plus S18–S24.`

Expected behavior: inspect inputs, construct competitive reference, run repository-native species-resolved analysis, use **all four required plugins** for their assigned checkpoints, validate RP/Bath pathway membership before freezing gene sets, separate RP comparative inference from Bath descriptive support, generate outputs, and flag unresolved boundaries.

## Negative control

Input: `Rewrite this paragraph about cbbL expression for the Discussion.`

Expected behavior: do not launch the full RNA-seq workflow solely because a transcriptomic gene is mentioned.

## Maturity

Status: **experimental / specification-complete, not yet forward-validated on the actual FASTQ dataset**.

Promote to `stable / forward-validated once` only after one complete real-data run verifies species assignment, all four plugin checkpoints, database-backed module validation, RP differential analysis, Bath support metrics, figure-source traceability, and evidence boundaries.
