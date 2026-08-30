# PR-CAL Evidence-Calibrated Scientific Inference Workflow

Use this specialist workflow under `PR-RSCH` when reviewing or rewriting scientific claims, mechanism interpretations, discussion sections, conclusions, abstracts, or near-final research manuscripts.

`PR-CAL` is **not** a top-level PR class. The authoritative object remains academic research content, so the primary class remains `PR-RSCH`.

## Purpose

Prevent two symmetric review errors:

1. **overclaiming** — expressing a conclusion more strongly than the evidence supports; and
2. **underclaiming / over-conservatism** — weakening or rejecting a scientifically supportable conclusion merely because no single assay independently proves the full mechanism.

The target is the **strongest defensible claim**, not the most cautious possible sentence.

## Core rule: claim corridor

For each material claim, determine both boundaries:

- **upper bound** — the strongest conclusion that the available evidence can defend without adding unsupported causality, species attribution, mechanism specificity, or generality;
- **lower bound** — the weakest wording below which the text would materially understate convergent evidence, verified perturbation effects, reproducible patterns, or well-supported interpretation.

Choose wording inside this corridor. Prefer the strongest wording that remains within the upper bound.

Do not treat caution itself as evidence of rigor.

## Global empirical mechanism envelope

Use the maintained experimental-paper corpus as the external calibration boundary for mechanism claims.

The model's generic caution level is not the authority. A mechanism interpretation should **not** be rejected merely because an exact same-system, same-journal, or nearest-neighbour precedent is absent, provided that the mechanism layer and wording remain within the empirical range represented across the active corpus and the manuscript's own evidence supports that position.

### Two-stage calibration

Separate two questions:

1. **Global external boundary — what kinds and strengths of mechanism claims are empirically represented in the corpus?**
2. **Local evidential position — where inside that global boundary does the manuscript's own evidence place the claim?**

The full active corpus defines the outer empirical mechanism envelope. Local evidence determines the claim's defensible position inside it.

Do not require a disputed mechanism claim to reproduce the exact evidence architecture of a small subset of papers before it can fall within the published mechanism envelope.

### Global corpus procedure

For central or disputed claims:

1. identify the claim layer: observed phenomenon, system-level function, mechanism, route identity, species attribution, or exact flux/causal step;
2. identify whether that mechanism layer and comparable wording strength occur anywhere within the active experimental corpus;
3. inspect the range of evidence packages associated with that layer across the corpus, including defined coculture, controls, isotope tracing, perturbation, genetics, electrochemistry, metabolite measurements, omics, microscopy, time course, incapacity controls, or other functional evidence;
4. determine whether the manuscript's own evidence is sufficient to place the claim somewhere within that published range;
5. retain narrower unresolved boundaries explicitly when the manuscript does not resolve species attribution, exact carrier, route identity, flux, or causality;
6. flag overclaim only when the claim exceeds both the manuscript's local evidential support and the global empirical mechanism envelope, or when it imports a narrower attribution that the data do not support;
7. flag underclaim when the manuscript is forced materially below a mechanism layer that is supported by its own convergent evidence and falls within the global empirical envelope.

Exact target-journal matches and close analogues may be consulted as contextual examples, but they are **not hard prerequisites** for a mechanism claim to be considered within the acceptable empirical range.

### Corpus membership is not automatic permission

A paper in the corpus with unusually strong evidence does not automatically license the same wording for weaker local evidence.

For example:

- a genetic knockout plus isotope tracing may justify `demonstrates` for a specific causal step;
- the existence of that published `demonstrates` statement shows that this mechanism layer lies inside the global corpus envelope;
- a manuscript lacking the isolating intervention may still need `supports`, `indicates`, or `is consistent with` for that same layer.

Thus, **global corpus membership defines the outer boundary; local evidence calibrates the exact verb and specificity inside that boundary**.

Do not use one published overclaim as automatic permission to overstate weak local evidence, but also do not let the absence of an exact precedent create an artificially narrow bar.

## Maintained empirical corpus requirement

Maintain a reusable benchmark corpus with at least **50 active, relevant experimental studies**. Prefer a baseline of **60 or more** so that removal of weak, outdated, or poorly matched samples does not collapse coverage.

The corpus should be diversified across the main journal families used for the research program rather than dominated by one venue. For the current environmental microbiology/engineering profile, maintain substantial coverage from:

- **The ISME Journal**;
- **Environmental Science & Technology**;
- **Water Research**; and
- relevant **Nature Portfolio** comparators.

Each active corpus entry should record, at minimum:

- journal and year;
- experimental system;
- evidence architecture;
- focal claim layer;
- published claim-strength band;
- narrower limitation or unresolved layer retained by the authors; and
- why the sample is transferable to PR-CAL calibration.

The corpus is interpreted as a **global published mechanism envelope**, not by majority vote and not by mandatory nearest-neighbour matching.

Remove or down-weight samples that are review articles, commentary, obvious outlier claims unsupported by their own reported evidence, or papers that do not provide an interpretable evidence-to-claim relationship.

## Journal-family interpretation

Journal-specific examples may help with rhetoric, convention, or expected terminology, but they do not define a narrower mechanism ceiling than the full active corpus unless the user explicitly requests a journal-specific constraint.

Across environmental microbiology and engineering journals, common empirical patterns include:

- process + orthogonal molecular/physiological evidence can justify `supports`, `indicates`, `promotes`, or `facilitates` when the mechanism remains properly bounded;
- a system-level process may be `demonstrated` even when the exact interspecies route is only `suggested` or `supported`;
- strong perturbations such as knockout, incapacity controls, selective inhibition/rescue, physical separation, isotope tracing, or route-specific interventions can move a claim toward `shows`, `demonstrates`, or direct causal language for the layer they actually isolate;
- missing species-resolved or flux-resolved evidence usually limits the **species/flux-specific layer**, not necessarily the broader system-level interpretation;
- omics alone rarely establishes mechanism, but omics combined with functional/process evidence can materially strengthen a bounded mechanism claim.

## No single-assay veto

Do not classify a claim as unsupported solely because one ideal direct experiment is absent.

A mechanistic or interpretive claim may be supportable when multiple sufficiently independent lines of evidence converge, provided that:

- the observations are genuinely relevant to the same proposition;
- they are not merely repeated measurements of the same underlying signal;
- major alternative explanations have been considered;
- the wording reflects what remains unresolved;
- missing direct evidence is stated as a limitation when material.

The absence of species-resolved, flux-resolved, or causal evidence should limit the **specificity** of the claim, not automatically erase support for a broader system-level or mechanism-consistent conclusion.

## Evidence triangulation card

For each important claim, build a compact evidence card:

```text
Claim:
Claim layer:
Global corpus mechanism range:
Relevant corpus precedents/examples:
Direct evidence:
Perturbation / intervention evidence:
Temporal or dose-response evidence:
Orthogonal physiological / molecular / chemical evidence:
Relevant controls:
Alternative explanations tested or weakened:
Evidence dependencies / shared measurement basis:
Important missing evidence:
Local position inside global envelope:
Strongest defensible claim:
Claims that remain too strong:
```

Do not count evidence lines by number alone. Weight their independence, relevance, directionality, and susceptibility to shared bias.

## Evidence tiers

Use the following working tiers for local placement inside the global empirical mechanism envelope.

### Tier 1 — Directly demonstrated

The relevant variable, species, flux, causal step, or mechanism was directly measured or experimentally isolated with appropriate controls.

Appropriate language may include:

- `demonstrates`;
- `shows`;
- `establishes`;
- direct causal wording when the intervention genuinely isolates causality.

### Tier 2 — Strongly supported by convergent evidence

No single experiment isolates the entire mechanism, but multiple independent or orthogonal observations converge and meaningful alternatives are weakened.

Appropriate language may include:

- `supports`;
- `strongly supports`;
- `provides evidence for`;
- `is consistent with a model in which`;
- `collectively indicates`;
- `supports the interpretation that`;
- `promotes` or `facilitates` when the functional evidence supports that level within the global empirical envelope.

Do **not** automatically downgrade Tier 2 to `speculative`, `unsupported`, or `cannot conclude` merely because Tier 1 evidence is absent.

### Tier 3 — Plausible interpretation

Evidence is relevant and directionally consistent, but key alternatives remain viable or evidence streams are strongly dependent.

Appropriate language may include:

- `suggests`;
- `is consistent with`;
- `may reflect`;
- `is compatible with`.

### Tier 4 — Hypothesis / unresolved inference

The proposition is scientifically plausible but weakly constrained by the current data.

Use explicit hypothesis language and identify the experiment needed to discriminate it.

## Independence check

Before calling several observations "multiple lines of evidence," ask whether they are actually independent.

Examples of partially dependent evidence:

- the same raw measurement shown as concentration, percent change, and fold change;
- several derived metrics calculated from one underlying assay;
- two readouts that share the same denominator or normalization artifact;
- repeated descriptions of the same temporal trend.

Examples of stronger triangulation:

- phenotype + metabolite dynamics + targeted perturbation;
- isotope incorporation + physiological controls + independently measured metabolic response;
- temporal association + intervention that selectively weakens the proposed coupling;
- molecular evidence + functional phenotype + orthogonal chemical measurement.

## Alternative-explanation gate

Do not require every imaginable alternative to be experimentally excluded.

Instead classify alternatives as:

- **material and viable** — would materially change the interpretation and remains compatible with the data;
- **partially weakened** — evidence argues against it but does not exclude it;
- **substantially weakened** — multiple observations or controls make it unlikely within the current experimental context;
- **not relevant to the specific claim**.

Only material viable alternatives should strongly limit claim strength.

## Positive scientific language gate

When evidence supports a conclusion, prefer affirmative scientific writing over reflexive negation.

Prefer:

- `These results support...`
- `The combined evidence indicates...`
- `This pattern is consistent with...`
- `The perturbation further supports...`
- `Together, the observations support a model in which...`

when justified.

Avoid unnecessary constructions such as:

- `it cannot be concluded that...` when a narrower positive conclusion is supported;
- `there is insufficient evidence to say anything about...` when the evidence supports a bounded interpretation;
- `only suggests` when `supports` is justified by convergent evidence;
- repeating limitations in every sentence after they have already been clearly bounded.

A limitation should define the boundary of the conclusion, not erase the conclusion.

## Severity calibration for review findings

Do not assign high-severity labels merely because evidence is indirect or because one ideal assay is absent.

Use:

- **P0 / critical** — factual/data contradiction, invalid calculation, central claim outside both the local evidence boundary and the global empirical mechanism envelope, materially false species/causal attribution, or conclusion incompatible with the evidence;
- **P1 / major** — claim materially exceeds or understates the defensible local position inside the global corpus envelope, important alternative explanation ignored, or a central inference needs substantial recalibration;
- **P2 / moderate** — wording strength, local evidence linkage, or uncertainty framing can be improved without changing the main scientific interpretation;
- **P3 / minor** — stylistic precision or optional strengthening/softening.

A claim that is supported by convergent evidence but lacks a single direct assay should not be labeled P0 solely for that reason.

If the global corpus contains established mechanism claims at the relevant layer and the manuscript's evidence supports a bounded version of that layer, forcing the manuscript to remain purely agnostic may itself warrant a P1/P2 **underclaim** finding.

## Bath–RP / environmental microbiology examples

Apply the existing `PR-RSCH` evidence boundaries, but calibrate them symmetrically inside the global empirical mechanism envelope.

Examples:

- Bulk community EA-IRMS does not establish RP-specific inorganic-carbon incorporation. However, it can directly support **community-level inorganic carbon incorporation**, and in combination with RP physiology, perturbation, and other orthogonal evidence may support a bounded interpretation about partner-associated metabolic coupling.
- Metabolite depletion alone does not establish a Bath-to-RP flux. However, production/consumption patterns, RP substrate-use controls, donor perturbation, and temporal coupling may collectively support **diffusible metabolite exchange as a mechanism-consistent interpretation** without naming one carrier as uniquely causal.
- A GAC-associated enhancement alone does not demonstrate DIET. A stronger DIET claim requires conductive-interface and alternative-pathway evidence; nevertheless, multiple conductive-material and perturbation results may justify `consistent with potential GAC-facilitated electron coupling` or stronger wording when the local evidence places the claim within a mechanism layer already represented by the global corpus.

## Review output

For central claims, report both overclaim and underclaim risk:

| Claim | Global corpus mechanism range | Local evidence tier | Convergent evidence | Main unresolved boundary | Overclaim risk | Underclaim risk | Recommended wording strength |
| --- | --- | --- | --- | --- | --- | --- | --- |

When criticizing a claim, provide the strongest acceptable replacement rather than only saying what cannot be claimed.

## Relationship to other specialist workflows

- `PR-RSCH` remains the primary scientific-review profile.
- `PR-CAL` calibrates evidence strength and inference.
- `PR-AUTH` handles authorship/style/AI-writing integrity and meaning preservation.
- `PR-DATA` should be added when a claim depends on deterministic recalculation or source-data verification.
- `PR-DOC` should be added only for native document QA.

Do not use `PR-MIX` merely because several validation overlays are active.

## Completion criteria

A research review passes `PR-CAL` when:

- both overclaim and underclaim risks were considered;
- important conclusions were evaluated using the full evidence set rather than one assay in isolation;
- the maintained empirical corpus contains at least 50 active, relevant experimental studies, with 60+ preferred for robust coverage;
- the **full active corpus** was treated as the outer empirical mechanism boundary rather than imposing a narrower mandatory same-journal or nearest-neighbour boundary;
- exact target-journal or close-analogue papers were used only as contextual aids unless the user explicitly requested a journal-specific constraint;
- local evidence was still used to determine the exact verb, specificity, attribution, and causal strength inside that global boundary;
- corpus membership was not treated as automatic permission to borrow stronger wording than the manuscript's own evidence supports;
- apparent multiple evidence lines were checked for dependence;
- material alternative explanations were identified proportionately;
- limitations define the claim boundary without unnecessarily erasing supported conclusions;
- central claims use the strongest defensible wording within the manuscript's local evidential position and the global empirical mechanism envelope;
- severe unsupported-claim labels are not assigned solely because one ideal direct assay is missing;
- each major criticism includes a scientifically supportable positive replacement where possible.
