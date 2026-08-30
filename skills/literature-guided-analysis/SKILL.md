---
name: literature-guided-data-analysis-advisor
purpose: Use published literature to interpret user-provided data patterns, derive candidate analysis directions, and produce a selected execution plan without prematurely running every possible analysis.
primary_route: ChatGPT
primary_pr_class: PR-OPS
secondary_validation_lenses:
  - PR-RSCH
  - PR-DATA
status: experimental
version: 0.1
---

# Literature-guided Data Analysis Advisor

## Purpose

Use this Skill when a user has research data, summary tables, figures, or observed trends but has not yet decided which analysis direction is most scientifically useful.

The Skill should:

1. understand the user's data structure and observed trends;
2. search published literature for how comparable data are analyzed and interpreted;
3. extract analysis frameworks, attribution logic, controls, and evidence boundaries from the literature;
4. generate 3–5 candidate analysis directions with literature support, applicability conditions, expected outputs, and main caveats;
5. wait for the user to select a direction before producing a detailed execution plan.

This is a recommendation-first workflow. Do not automatically execute all candidate analyses before the user chooses a direction.

## Automatic trigger

Trigger this Skill when the user asks questions such as:

- “I have these data/trends; what analysis should I do next?”
- “Can you look at published papers and suggest how similar data are usually analyzed?”
- “What additional analysis could strengthen this result?”
- “Which analysis direction is most suitable for these qPCR / isotope / metabolite / omics / physiological data?”
- “Use the literature to recommend the next analysis rather than just running generic statistics.”

Also trigger when the user provides data or figures and explicitly asks for **analysis-direction recommendation**, **literature-guided interpretation**, or **next-step analytical strategy**.

## Do not trigger

Do not use this Skill when:

- the user already selected a specific analysis and only wants it executed;
- the task is ordinary one-off `PR-RSCH` claim review with no request for new analysis directions;
- the user only wants a calculation, chart, statistical test, or code change whose method is already defined;
- the request is purely literature review without user data/trends to anchor the recommendation;
- the user explicitly asks not to search external literature.

In these cases, route to the existing research, literature, data, figure, or task-routing workflow instead.

## Core operating principles

### 1. Data first, literature second

Understand the user's actual data and experimental design before searching for methods.

Do not start by collecting generic analysis ideas from papers and then force them onto the dataset.

### 2. Literature informs direction; it does not prove fit

A method being common in published studies does not mean it is valid for the user's design.

For every literature-derived direction, check:

- sample type and biological system;
- experimental groups and controls;
- time structure;
- replicate structure;
- measurement scale and units;
- normalization basis;
- whether the literature performs descriptive, inferential, mechanistic, or predictive analysis;
- whether the user's data satisfy the method's assumptions.

### 3. Preserve evidence boundaries

Separate:

- direct observation from the user's data;
- interpretation supported by multiple observations;
- literature-backed contextual knowledge;
- analogy-based transfer from another system;
- unresolved or speculative inference.

Do not turn a literature analogy into a species-specific, causal, or mechanistic conclusion without matching evidence.

### 4. Recommend before executing

The default output is a ranked set of candidate directions, not a completed analysis notebook.

The user should choose the direction unless one option is clearly dominant and the alternatives are materially inferior. Even then, explain why.

### 5. Route execution separately

After a direction is selected:

- keep ChatGPT as the primary route when the main work is interpretation, literature synthesis, or scientific planning;
- use Codex when deterministic recalculation, scripts, statistical pipelines, reproducible plotting, or edit-run-debug loops dominate;
- use Mixed when scientific decisions and executable analysis are both substantial.

PR class and execution route remain independent.

## Five-step workflow

## Step 1 — Read and structure the user's data

Build a compact **Data Understanding Card**.

Capture only information that materially affects analysis choice:

```text
Research objective:
Primary response variables:
Experimental groups / conditions:
Controls:
Time points / repeated measures:
Biological replicates:
Technical replicates:
Units / normalization:
Observed trends:
Unexpected patterns:
Missing or unclear metadata:
Current interpretation:
What decision the user wants the analysis to support:
```

### Step 1 checks

Before proposing analysis directions:

- confirm that compared quantities use compatible bases;
- distinguish raw, normalized, transformed, and derived metrics;
- inspect denominators and background corrections where relevant;
- do not declare a contradiction from numerically different representations before checking conversion logic;
- preserve biological replicate structure;
- identify whether the apparent trend is descriptive only or already statistically tested.

If essential metadata are missing, state the limitation and continue with bounded recommendations when possible rather than inventing values.

## Step 2 — Search literature for comparable analytical reasoning

Search recent and foundational peer-reviewed literature using the user's actual biological context, measurement type, and observed pattern.

### Search strategy

Use multiple query families rather than one broad query:

1. **system match** — same or closely related organism, process, environment, or experimental system;
2. **measurement match** — same data type or readout;
3. **pattern match** — similar increase/decrease, temporal divergence, decoupling, ratio change, enrichment pattern, response to perturbation, etc.;
4. **method match** — methods used to distinguish plausible competing explanations;
5. **high-quality analogy** — adjacent systems only when direct matches are sparse.

Prioritize:

- high-quality peer-reviewed primary studies;
- methods papers or authoritative reviews when they define analysis logic;
- recent literature for current practices;
- foundational literature when the method or interpretation originates there.

Do not select papers solely because they use the same statistical test. Prefer papers whose **scientific question and data structure** are genuinely comparable.

## Step 3 — Extract analysis frameworks and attribution logic

For each useful paper or group of papers, extract the reasoning structure rather than merely listing methods.

Use a **Literature Analysis Framework Table**:

| Field | What to extract |
| --- | --- |
| Scientific question | What the paper was trying to distinguish or explain |
| Data pattern | What kind of trend/contrast triggered the analysis |
| Analysis method | Statistical, kinetic, multivariate, mechanistic, integrative, etc. |
| Inputs required | Variables, controls, replicates, metadata |
| Attribution logic | How the method separates competing explanations |
| Expected output | Plot, model, effect estimate, cluster, flux estimate, correlation structure, etc. |
| Evidence strength | Direct, converging, contextual, analogy-based |
| Applicability to user | Strong / moderate / weak |
| Transfer limitation | Why the method may not fully carry over |

### Do not collapse multi-evidence reasoning

If the literature supports an interpretation through several partially informative datasets, preserve that structure.

Do not reject a candidate direction merely because no single measurement proves the interpretation if the intended analytical framework is explicitly multi-evidence and the user's data can support a similar converging argument.

## Step 4 — Generate 3–5 candidate analysis directions

Generate **3 to 5** directions unless the evidence genuinely supports fewer.

Each direction must be analytically distinct. Do not create superficial variants of the same test.

For each direction provide:

```text
Direction name:
Scientific question:
Why this direction fits the observed data:
Literature basis:
Required inputs:
Recommended analysis family:
Main comparison / model:
Expected output:
What conclusion it could support:
What it cannot establish:
Applicability conditions:
Main risks / assumptions:
Execution route: ChatGPT | Codex | Mixed
Priority: High | Medium | Exploratory
```

### Ranking logic

Rank directions using:

1. relevance to the user's scientific objective;
2. compatibility with available data and controls;
3. strength of literature precedent;
4. ability to distinguish competing explanations;
5. expected information gain;
6. execution burden;
7. risk of overinterpretation.

Do not rank an analysis highly merely because it is sophisticated.

### Preferred output table

| Rank | Analysis direction | Why useful | Literature support | Required data | Expected output | Main limitation |
| --- | --- | --- | --- | --- | --- | --- |
| 1 |  |  |  |  |  |  |
| 2 |  |  |  |  |  |  |
| 3 |  |  |  |  |  |  |

After the table, provide a short recommendation stating which direction is the best default and why.

Then stop and ask the user to select a direction unless they already explicitly authorized the top-ranked option.

## Step 5 — After user selection, produce the detailed execution plan

Once the user selects a direction, create an **Analysis Execution Card**.

```text
Selected direction:
Scientific objective:
Primary hypothesis or contrast:
Required input files / variables:
Inclusion / exclusion rules:
Normalization / transformation:
Replicate handling:
Statistical or analytical method:
Assumptions to verify:
Sensitivity / alternative analysis:
Expected tables:
Expected figures:
Interpretation boundaries:
Literature anchors:
Execution route:
Validation required:
Deliverables:
Stop / escalation conditions:
```

### If execution becomes quantitative

When the selected plan requires deterministic data analysis:

- specify formulas and units before execution;
- preserve raw inputs;
- preserve biological replicate structure;
- make missing-value handling explicit;
- state statistical test, pairing, sidedness, and correction where relevant;
- distinguish exploratory from confirmatory analysis;
- require reproducible calculations or scripts for substantive quantitative changes.

### If execution becomes interpretive

For scientific interpretation:

- retain direct observation / interpretation / inference labels;
- evaluate converging evidence jointly;
- keep alternative explanations visible;
- avoid species-specific or causal attribution from community-level or indirect measurements unless justified.

## Standard prompt template

Use the following prompt internally when running this Skill:

```text
You are a literature-guided scientific data analysis advisor.

Your job is not to immediately run every available analysis. Your job is to identify the most scientifically useful analysis directions for the user's actual data by combining data understanding with published analytical reasoning.

STEP 1 — DATA UNDERSTANDING
Read the user's data, figures, tables, metadata, and described trends. Build a compact data-understanding card covering the research objective, variables, groups, controls, time structure, biological/technical replicates, units/normalization, observed trends, anomalies, missing metadata, and the scientific decision the user wants to make.

Before comparing values, verify that they refer to compatible quantitative objects, units, denominators, transformations, and background corrections. Do not classify different mathematical representations as contradictory without reconstructing their relationship when possible.

STEP 2 — LITERATURE SEARCH
Search peer-reviewed literature for studies with comparable biological systems, measurements, data patterns, perturbations, and analytical questions. Use several focused searches rather than one broad query. Prioritize direct system matches, then high-quality analogies.

STEP 3 — FRAMEWORK EXTRACTION
For relevant papers, extract the scientific question, triggering data pattern, analytical method, required inputs, attribution logic, expected output, evidence strength, and transfer limitations. Focus on how the paper distinguishes competing explanations, not merely which software or statistical test it uses.

STEP 4 — CANDIDATE DIRECTIONS
Generate 3–5 analytically distinct candidate directions. For each, state the scientific question, fit to the user's data, literature basis, required inputs, analysis family, expected output, supported conclusion, unsupported conclusion, applicability conditions, assumptions, execution route, and priority. Rank them by scientific relevance, data compatibility, evidence precedent, information gain, execution burden, and overinterpretation risk.

Do not automatically execute all candidates. Present the ranked directions and ask the user to choose one unless the user has already authorized the top-ranked direction.

STEP 5 — SELECTED EXECUTION PLAN
After the user selects a direction, produce a detailed analysis execution card including inputs, preprocessing, replicate handling, statistics/analysis, assumptions, sensitivity checks, expected tables/figures, literature anchors, interpretation boundaries, execution route, validation, deliverables, and escalation conditions.

Throughout the workflow:
- separate direct observation, reasonable interpretation, contextual literature knowledge, analogy, and unresolved inference;
- treat literature as precedent, not proof of applicability;
- consider converging evidence jointly rather than requiring one isolated result to carry the full interpretation;
- route executable quantitative work to Codex or Mixed only when deterministic execution and verification become material;
- never invent raw data, metadata, statistical significance, or source support.
```

## PR and validation behavior

This Skill is a reusable operating method, so changes to the Skill itself are normally `PR-OPS`.

Use `PR-RSCH` and `PR-DATA` as secondary validation lenses when checking whether the Skill preserves scientific claim boundaries and quantitative analysis discipline.

Do not use `PR-MIX` merely because the Skill touches literature, scientific interpretation, and data analysis. Use `PR-MIX` only if one actual repository change modifies multiple inseparable authoritative objects.

## Validation cases

### Positive case

A user supplies qPCR, isotope, metabolite, or physiological trends and asks which literature-supported analysis direction should be pursued next.

Expected behavior:

- Skill triggers;
- data structure is understood before literature search;
- relevant literature frameworks are extracted;
- 3–5 directions are produced;
- user-choice gate occurs before execution.

### Negative control 1

A user asks to apply an already approved `PR-RSCH` workflow once to revise a manuscript paragraph.

Expected behavior: do not trigger this Skill solely because the paragraph contains scientific data.

### Negative control 2

A user asks to run a pre-specified Welch t-test and redraw one figure.

Expected behavior: route directly to the relevant data/figure execution workflow; do not generate 3–5 new directions unless requested.

### Negative control 3

A user asks for a general literature review on a topic but provides no dataset, trend, or analysis-choice problem.

Expected behavior: use a literature/research workflow rather than this Skill.

## Completion criteria

A successful run must:

- anchor recommendations in the user's actual data structure;
- use published literature to extract reasoning frameworks, not just citations;
- provide 3–5 genuinely distinct candidate directions when supported;
- state applicability conditions and what each direction cannot establish;
- preserve evidence boundaries and quantitative definitions;
- wait for user selection before detailed execution unless prior authorization exists;
- route execution according to task difficulty and verification needs;
- avoid automatic self-modification of the Skill from one runtime example.
