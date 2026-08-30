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

## Target-journal empirical calibration gate

When the target journal or journal family is known, calibrate the claim corridor against **published experimental papers with comparable evidence architecture** before assigning claim-strength severity to a central conclusion.

The model's generic caution level is not the authority. The practical bar is the mainstream evidence-to-language envelope accepted by the target journal for comparable work.

### Journal benchmark procedure

For central or disputed claims:

1. identify the target journal or nearest journal family;
2. retrieve at least **3 relevant experimental papers** when practical, preferably **5 or more** for a major mechanistic claim;
3. prioritize papers similar in scientific question, experimental design, evidence architecture, and mechanism depth rather than papers that merely use the same statistical test;
4. record which evidence types were available, such as defined coculture, controls, isotope tracing, perturbation, genetics, electrochemistry, metabolite measurements, omics, microscopy, time course, or functional incapacity controls;
5. record the actual claim verbs and scope used by the authors, distinguishing phenomenon-level, system-level mechanism, route identity, species attribution, and exact flux;
6. infer the **mainstream accepted claim-strength envelope** across the cohort rather than copying the boldest paper;
7. compare the manuscript claim against that empirical envelope.

Use target-journal papers as calibration evidence, not as permission to reproduce unsupported wording. A published overclaim is not automatically a valid precedent.

### Maintained empirical corpus requirement

Maintain a reusable target-journal benchmark corpus with at least **50 active, relevant experimental studies**. Prefer a baseline of **60 or more** so that removal of weak, outdated, or poorly matched samples does not collapse coverage.

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

For a disputed central mechanism claim, do not average the entire corpus. Retrieve the closest empirical neighbours. When practical, use at least **5 close analogues**, including at least **3 papers from the exact target journal** when suitable samples exist.

Corpus membership is evidence for calibration, not authority by majority vote. Remove or down-weight samples that are review articles, commentary, weak topic matches, obvious outlier claims, or papers whose evidence architecture is materially different from the manuscript under review.

### Journal-family interpretation

For environmental microbiology and engineering, use relevant papers from journals such as **The ISME Journal, Environmental Science & Technology, Water Research**, and appropriate Nature-family comparators when they match the evidence architecture.

Common empirical patterns include:

- process + orthogonal molecular/physiological evidence can justify `supports`, `indicates`, `promotes`, or `facilitates` when the mechanism remains properly bounded;
- a system-level process may be `demonstrated` even when the exact interspecies route is only `suggested` or `supported`;
- strong perturbations such as knockout, incapacity controls, selective inhibition/rescue, physical separation, isotope tracing, or route-specific interventions can move a claim toward `shows`, `demonstrates`, or direct causal language for the layer they actually isolate;
- missing species-resolved or flux-resolved evidence usually limits the **species/flux-specific layer**, not necessarily the broader system-level interpretation;
- omics alone rarely establishes mechanism, but omics combined with functional/process evidence can materially strengthen a bounded mechanism claim.

When the manuscript's wording is materially weaker than comparable published papers with a similar or stronger evidence package, flag **underclaim risk**. When it is materially stronger, flag **overclaim risk**.

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
Target journal / journal family:
Comparable published evidence packages:
Direct evidence:
Perturbation / intervention evidence:
Temporal or dose-response evidence:
Orthogonal physiological / molecular / chemical evidence:
Relevant controls:
Alternative explanations tested or weakened:
Evidence dependencies / shared measurement basis:
Important missing evidence:
Published wording envelope:
Strongest defensible claim:
Claims that remain too strong:
```

Do not count evidence lines by number alone. Weight their independence, relevance, directionality, and susceptibility to shared bias.

## Evidence tiers

Use the following working tiers for claim calibration. These tiers are defaults and should be adjusted within the target-journal empirical envelope when a benchmark is available.

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
- `promotes` or `facilitates` when a target-journal benchmark shows that the functional evidence package supports that level.

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

- **P0 / critical** — factual/data contradiction, invalid calculation, unsupported central claim, materially false species/causal attribution, or conclusion incompatible with the evidence and target-journal evidence envelope;
- **P1 / major** — claim materially exceeds or understates the defensible evidence corridor, important alternative explanation ignored, or a central inference needs substantial recalibration;
- **P2 / moderate** — wording strength, local evidence linkage, or uncertainty framing can be improved without changing the main scientific interpretation;
- **P3 / minor** — stylistic precision or optional strengthening/softening.

A claim that is supported by convergent evidence but lacks a single direct assay should not be labeled P0 solely for that reason.

If comparable target-journal papers routinely use stronger bounded wording for a similar evidence architecture, a weaker manuscript statement may itself warrant a P1/P2 **underclaim** finding.

## Bath–RP / environmental microbiology examples

Apply the existing `PR-RSCH` evidence boundaries, but calibrate them symmetrically and against relevant target-journal precedent when available.

Examples:

- Bulk community EA-IRMS does not establish RP-specific inorganic-carbon incorporation. However, it can directly support **community-level inorganic carbon incorporation**, and in combination with RP physiology, perturbation, and other orthogonal evidence may support a bounded interpretation about partner-associated metabolic coupling.
- Metabolite depletion alone does not establish a Bath-to-RP flux. However, production/consumption patterns, RP substrate-use controls, donor perturbation, and temporal coupling may collectively support **diffusible metabolite exchange as a mechanism-consistent interpretation** without naming one carrier as uniquely causal.
- A GAC-associated enhancement alone does not demonstrate DIET. A stronger DIET claim requires conductive-interface and alternative-pathway evidence; nevertheless, multiple conductive-material and perturbation results may justify `consistent with potential GAC-facilitated electron coupling` or stronger wording if the complete evidence package matches accepted target-journal precedent.

## Review output

For central claims, report both overclaim and underclaim risk:

| Claim | Target-journal benchmark | Evidence tier | Convergent evidence | Main unresolved boundary | Overclaim risk | Underclaim risk | Recommended wording strength |
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
- central disputed claims were benchmarked against comparable target-journal papers when the target journal was known and such papers were available;
- the maintained empirical corpus contains at least 50 active, relevant experimental studies, with 60+ preferred for robust coverage;
- the benchmark used close empirical neighbours rather than averaging the full corpus or relying on one bold outlier;
- for major disputed mechanism claims, at least 5 close analogues were used when practical, including at least 3 from the exact target journal when suitable samples existed;
- apparent multiple evidence lines were checked for dependence;
- material alternative explanations were identified proportionately;
- limitations define the claim boundary without unnecessarily erasing supported conclusions;
- central claims use the strongest defensible wording within both the evidence corridor and the target-journal empirical envelope;
- severe unsupported-claim labels are not assigned solely because one ideal direct assay is missing;
- each major criticism includes a scientifically supportable positive replacement where possible.
