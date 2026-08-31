# Pathway and Functional-Module Database Validation Workflow

Canonical key: `WF-PATHWAY-VALIDATE`

Use this workflow before a curated pathway/module is used for enrichment, selected-gene visualization, mechanistic interpretation, or a main-text model in transcriptomic analysis.

The purpose is to prevent pathway labels from being accepted only because they were proposed in advance, inherited from a single annotation source, or returned by an enrichment tool.

## Trigger

Run this workflow when a task:

- builds or revises a curated gene set/module;
- assigns genes to a mechanism-critical pathway;
- uses pathway membership to interpret RNA-seq results;
- prepares a selected-gene heatmap or mechanistic model from pathway/module membership;
- resolves conflicting or uncertain bacterial gene annotations.

For `WF-RNA-DUAL`, this workflow is mandatory before finalizing RP modules in Phase 5 and Bath modules in Phase 6.

## Core rule

A pathway/module must be supported by an auditable chain from **organism-specific gene identity → molecular function/reaction → pathway/module role**.

Do not treat a pathway name returned by GSEA/KEGG/GO/STRING as proof that every included gene performs the proposed mechanism in the target organism.

## Preferred evidence hierarchy

Use the strongest organism-specific sources available. The default order is:

1. **Authoritative genome annotation** for the exact strain/accession used in the analysis.
2. **Life Sciences Databases / UniProt** for gene/protein identity, reviewed or unreviewed functional annotation, EC numbers, domains, and cross-references.
3. **Life Sciences Databases / QuickGO** for GO molecular-function, biological-process, and ontology relationships when an appropriate annotation exists.
4. **Life Sciences Databases / Rhea** for biochemical reaction identity and reaction-direction/participant validation when the mechanism depends on a specific enzymatic reaction.
5. **KEGG, eggNOG, MetaCyc or equivalent pathway/orthology resources** when accessible in the execution environment, especially for pathway membership and orthology context.
6. **Life Sciences Databases / STRING** for enrichment, functional association, and neighborhood/context support. Treat STRING as contextual support, not sole proof of biochemical function.
7. **Life Sciences Databases / Reactome** only when a relevant species/event mapping exists. Do not transfer a human pathway definition directly to a bacterial gene without organism-specific support.
8. **Primary literature** for mechanism-critical genes/modules, unusual assignments, contradictory annotations, strain-specific functions, or claims central to the manuscript.
9. **Sequence/alignment evidence** when homolog assignment or cross-species identity remains ambiguous.

Absence from one database is not automatic evidence of absence. Record the lookup as unresolved and use another appropriate source.

## Required validation table

Create a machine-readable table such as `pathway_module_validation.tsv` with at least:

- species;
- module_id;
- proposed_module_name;
- gene_id / locus_tag;
- gene_symbol if available;
- reference-annotation description;
- UniProt accession / annotation status when available;
- GO terms relevant to the proposed role;
- EC number and/or Rhea reaction when applicable;
- pathway/orthology cross-reference when available;
- literature support when required;
- sequence/homology status when required;
- evidence class;
- include / exclude / provisional decision;
- rationale;
- conflict or uncertainty note.

## Evidence classes

Use a compact evidence classification:

- **A — direct organism-specific support**: exact strain/species annotation plus biochemical/pathway evidence consistent with the proposed role.
- **B — strong orthology/context support**: well-supported homolog/ortholog and consistent functional evidence, but no direct strain-specific characterization.
- **C — plausible / provisional**: partial annotation, context, or literature analogy supports inclusion but an important link remains unresolved.
- **X — unsupported/conflicting**: evidence does not support the proposed module assignment or conflicts materially with it.

Only A/B genes should define the **core** of a main-text curated module by default. C genes may be retained as provisional/extended members if explicitly labeled and if their inclusion does not drive the conclusion. X genes must be excluded unless the purpose is to show an annotation conflict.

## Module-level acceptance

Before a module is used in a main-text pathway plot or heatmap:

1. define the biological function the module is intended to represent;
2. list the encoded genes expected for that function in the target organism;
3. validate each mechanism-critical gene through the evidence hierarchy;
4. identify missing, duplicated, divergent, or ambiguous components;
5. separate core genes from optional/provisional genes;
6. record whether the module is complete, partial, or candidate in the genome;
7. freeze a versioned gene-set file before GSEA or figure generation.

Do not alter gene-set membership after seeing the desired enrichment direction unless the change is justified by new annotation evidence and documented as a versioned revision.

## Interpretation rules

- **GSEA/enrichment is downstream evidence**, not a pathway-definition tool by itself.
- GO terms can be broad; do not equate a parent GO biological process with a specific metabolite-transfer mechanism without gene-level evidence.
- EC/Rhea reaction support is especially important when distinguishing production versus consumption routes or alternative enzyme functions.
- Orthology does not guarantee identical physiological role under the experimental condition.
- Expression of a complete or near-complete pathway supports transcriptional capacity/activity, not metabolic flux.
- A partial pathway should be described as partial/candidate rather than converted into a complete mechanistic route in a figure.

## Bath–RP-specific priorities

For `WF-RNA-DUAL`, prioritize validation of:

### RP
- formate uptake/oxidation genes, including proposed `HZF03_03710–03730` members;
- H2 metabolism genes, including proposed `HZF03_04850–04865` members;
- `acs` and acetate activation;
- `nuo`, `pet/bc1`, terminal oxidases, ATP synthase, and `pntAB`;
- `cbbL`, `cbbS`, `cbbX`, `cbbM`, `prk/cbbP`;
- RuBP-regeneration genes included in the curated CBB module.

### Bath
- `pmoCAB` / `mmo` methane oxidation;
- `mxa/xox` methanol oxidation;
- RuMP-cycle genes;
- H4MPT-linked C1 oxidation genes;
- formate metabolism;
- candidate hydrogenase/H2 routes;
- riboflavin biosynthesis/export or redox-mediator-related genes;
- Bath CBB genes.

For genes central to the Bath→metabolite→RP model, require at least two compatible evidence sources when practical, with one being organism-specific annotation/sequence evidence.

## Outputs

A completed validation produces:

- `pathway_module_validation.tsv`;
- versioned RP and Bath gene-set files;
- a short conflict/unresolved list;
- source identifiers or links sufficient to reproduce the lookups;
- a record of database access date and database/release version when available.

## Completion gate

Do not call the pathway/module stage complete until:

- mechanism-critical genes have database-backed validation;
- main-text modules have frozen, auditable membership;
- provisional genes are visibly separated from core genes;
- unresolved annotation conflicts are carried forward rather than silently resolved;
- enrichment and figures are regenerated after the final gene-set version is frozen.

## Positive case

Input: `Validate the RP formate, H2, respiratory-energy and CBB modules before Fig. 3.5a/b.`

Expected behavior: query organism-specific annotations and Life Sciences Databases, verify molecular functions/reactions and pathway membership, classify each gene, freeze the validated modules, then permit enrichment/heatmap generation.

## Negative control

Input: `The volcano plot shows cbbL is significant; make it red.`

Expected behavior: do not launch full pathway validation unless pathway membership or mechanistic interpretation is being established/revised.

## Maturity

Status: **experimental / specification-complete**. Promote after one real Bath–RP transcriptomics run demonstrates that the validation table catches or resolves at least one meaningful annotation/module ambiguity without creating unnecessary analysis overhead.
