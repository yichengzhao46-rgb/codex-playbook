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
Direct evidence:
Perturbation / intervention evidence:
Temporal or dose-response evidence:
Orthogonal physiological / molecular / chemical evidence:
Relevant controls:
Alternative explanations tested or weakened:
Evidence dependencies / shared measurement basis:
Important missing evidence:
Strongest defensible claim:
Claims that remain too strong:
```

Do not count evidence lines by number alone. Weight their independence, relevance, directionality, and susceptibility to shared bias.

## Evidence tiers

Use the following working tiers for claim calibration:

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
- `supports the interpretation that`.

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

Do not assign high-severity labels merely because evidence is indirect.

Use:

- **P0 / critical** — factual/data contradiction, invalid calculation, unsupported central claim, materially false species/causal attribution, or conclusion incompatible with the evidence;
- **P1 / major** — claim materially exceeds or understates the defensible evidence corridor, important alternative explanation ignored, or a central inference needs substantial recalibration;
- **P2 / moderate** — wording strength, local evidence linkage, or uncertainty framing can be improved without changing the main scientific interpretation;
- **P3 / minor** — stylistic precision or optional strengthening/softening.

A claim that is supported by convergent evidence but lacks a single direct assay should not be labeled P0 solely for that reason.

## Bath–RP / environmental microbiology examples

Apply the existing `PR-RSCH` evidence boundaries, but calibrate them symmetrically.

Examples:

- Bulk community EA-IRMS does not establish RP-specific inorganic-carbon incorporation. However, it can directly support **community-level inorganic carbon incorporation**, and in combination with RP physiology, perturbation, and other orthogonal evidence may support a bounded interpretation about partner-associated metabolic coupling.
- Metabolite depletion alone does not establish a Bath-to-RP flux. However, production/consumption patterns, RP substrate-use controls, donor perturbation, and temporal coupling may collectively support **diffusible metabolite exchange as a mechanism-consistent interpretation** without naming one carrier as uniquely causal.
- A GAC-associated enhancement alone does not demonstrate DIET. A stronger DIET claim requires conductive-interface and alternative-pathway evidence; nevertheless, multiple conductive-material and perturbation results may justify `consistent with potential GAC-facilitated electron coupling` rather than forcing a purely agnostic description.

## Review output

For central claims, report both overclaim and underclaim risk:

| Claim | Evidence tier | Convergent evidence | Main unresolved boundary | Overclaim risk | Underclaim risk | Recommended wording strength |
| --- | --- | --- | --- | --- | --- | --- |

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
- apparent multiple evidence lines were checked for dependence;
- material alternative explanations were identified proportionately;
- limitations define the claim boundary without unnecessarily erasing supported conclusions;
- central claims use the strongest defensible wording within the evidence corridor;
- severe unsupported-claim labels are not assigned solely because one ideal direct assay is missing;
- each major criticism includes a scientifically supportable positive replacement where possible.
