# PR-AUTH Academic Authorship and AI-Writing Risk Workflow

Use this specialist checklist under `PR-RSCH` for **every substantive revision of academic prose**, including manuscripts, thesis or confirmation-report chapters, proposals, responses to reviewers, figure legends, abstracts, and conclusions.

`PR-AUTH` is **not** a PR class. The authoritative object remains academic prose,
so the primary class is normally `PR-RSCH`.

## Automatic trigger

Trigger `PR-AUTH` automatically whenever a task:

- revises, rewrites, condenses, expands, restructures, or harmonizes academic prose;
- changes the wording used to interpret research data, figures, tables, or mechanisms;
- adds or revises a manuscript/thesis argument, discussion, conclusion, abstract, caption, or objective;
- asks for academic-style improvement, AI-writing-risk reduction, or human-like but academically appropriate wording.

Do **not** wait for a separate user request to check academic style or AI-writing risk once substantive academic prose is being changed.

Non-trigger cases include purely mechanical formatting with no prose changes, deterministic calculations, code-only changes, or figure-layout-only edits that do not modify academic text.

## Governing priority

Apply the following precedence. Lower-priority goals must never override a
higher-priority requirement.

1. Scientific validity and evidence boundaries
2. Institutional and disciplinary academic-writing requirements
3. Author-specific academic voice and information density
4. Formulaic / AI-writing risk reduction

Never change claim strength, evidence attribution, species attribution, numerical
meaning, causal interpretation, citation relationship, or unresolved uncertainty
merely to reduce an AI-detector score or make prose appear more human-written.

## Authoritative references

For PolyU research writing, use both:

- the repository's `PR-RSCH` validation gate and evidence-boundary rules; and
- PolyU English Language Centre, **Academic Writing Style Guide**:
  https://elc.polyu.edu.hk/RPg/wr_guidelines_style.htm

Where a local assignment prompt, supervisor instruction, journal guide, rubric,
or project-specific rule conflicts with a generic style preference, follow the
more specific authoritative instruction unless it would violate scientific
accuracy or research integrity.

## Stage 0 — Original-safe editing gate

Before any tool or agent writes changes into a user document or repository file, establish a reversible editing path.

Default order of preference:

1. **Versioned revised copy:** keep the original file untouched and write a new file such as `name_revised_v1.docx`, `name_PR-AUTH_v1.docx`, or an equivalently clear versioned filename.
2. **Version-controlled branch:** for repository text files, make changes on a dedicated branch so the pre-edit version remains recoverable from Git history; do not edit the only copy directly on `main` for meaningful prose changes.
3. **Explicit backup before overwrite:** only when the workflow genuinely requires in-place editing, create and verify a backup copy before overwrite.

For Word/PDF deliverables, prefer **original + revised copy** over hidden in-place replacement. If tracked changes are specifically requested and supported, the tracked-change document may serve as the revised copy, but the original must still remain available.

If a backup/revised copy cannot be created or version-control recovery cannot be verified, stop before destructive overwrite and report the constraint.

Record in the task/PR output:

- original filename/path;
- revised filename/path or branch;
- whether the original was left untouched;
- how rollback/recovery is performed.

## Stage 1 — Meaning lock

Before rewriting, identify and lock the following where present:

- numerical values, units, statistical results, sample sizes, and time points;
- experimental groups, conditions, controls, and interventions;
- organism / species attribution;
- figure, table, section, and supplementary references;
- citations and which claim each citation supports;
- direct observations versus interpretations versus mechanistic inferences;
- uncertainty, limitations, unresolved controls, and alternative explanations.

If a proposed wording change alters one of these, treat it as a scientific edit
and return it to `PR-RSCH` review rather than silently accepting it as style work.

## Stage 2 — Scientific evidence audit

Classify material claims as one of:

- directly observed or experimentally verified;
- supported by multiple converging observations but not directly isolated;
- source-backed contextual knowledge;
- inferred or transferred by analogy;
- unresolved, speculative, or not checked.

Check that verbs and certainty match the evidence category. In particular, do
not replace cautious interpretations with causal or species-specific claims unless
the corresponding direct test exists.

### Quantitative consistency and false-conflict prevention

Before flagging two numerical statements as contradictory, establish that they
refer to the same quantitative object on the same basis. Check, where applicable:

- analyte or response variable;
- sample, treatment, replicate set, and time point;
- direct measurement versus transformed or derived quantity;
- numerator, denominator, sample mass, total-carbon basis, biomass basis, protein
  normalization, volume basis, or other sample-specific normalizer;
- background subtraction, blank correction, baseline correction, or natural-
  abundance correction;
- unit conversion, percentage versus fraction, logarithmic or isotopic notation,
  and rounding;
- whether two values are alternative mathematical representations of the same
  measurement rather than independent measurements.

Do not infer a data conflict merely because values differ numerically across
representations or derived metrics. Reconstruct the stated conversion or formula
first when the document provides enough information. If the required source data,
normalizer, or formula is unavailable, classify the item as **unresolved / needs
verification**, not as a confirmed contradiction.

For derived absolute quantities, inspect all quantity-dependent terms before
comparing magnitudes. A small difference in a concentration, fraction, enrichment,
or atom percentage can produce a non-zero absolute amount when multiplied by a
sample-specific mass or total content. Conversely, similar relative values can
produce different absolute amounts when sample totals differ.

Isotope example: `δ13C`, `atom% 13C`, and background-corrected absolute `13C
excess` are related but not interchangeable reporting layers. `δ13C` and `atom%
13C` can represent the same isotopic composition in different notation, whereas
absolute `13C excess` additionally depends on the amount of carbon in the analyzed
sample and the selected background correction. Do not classify these as mutually
inconsistent until the conversion, sample identity, total-carbon basis, and
background are aligned.

Use severity labels conservatively:

- **confirmed conflict** only when values remain incompatible after matching the
  same sample, basis, transformation, units, and calculation definition;
- **apparent discrepancy** when the mismatch may be explained by a different
  representation, denominator, normalization, or derived calculation;
- **needs source-data verification** when the manuscript alone cannot resolve the
  relationship.

If reconstruction requires raw data or deterministic recalculation, route the
item to the `PR-DATA` validation gate before escalating its scientific severity.

For Bath-RP / MOB-EET work, preserve the existing `PR-RSCH` constraints: do not
infer RP-specific carbon fixation from bulk community isotope incorporation, do
not assign mixed-community ATP/NAD(H) to RP, do not convert metabolite depletion
into a confirmed Bath-to-RP flux, and do not call a conductive-material response
DIET without the required evidence.

## Stage 3 — PolyU academic-style audit

Apply the PolyU ELC principles of formal, precise, clear, objective, and
well-organised academic writing.

### Avoid or repair when inappropriate

- informal phrasal verbs when a precise academic verb is available;
- colloquial expressions and conversational intensifiers;
- clichés and stock phrases that add little information;
- repetitive sentence-initial connectives;
- rhetorical questions in formal academic prose;
- run-on expressions such as `etc.` and `and so on` when they leave the set
  unspecified;
- informal contractions;
- unnecessary first-person `I`; use discipline-appropriate `we` only when it is
  rhetorically justified;
- awkward negative constructions when a clearer positive equivalent exists;
- vague terms such as `thing`, `something`, or an unspecified `someone`;
- ambiguous pronouns, especially unclear `it`, `this`, `these`, or `they`;
- subjective, emotional, or evaluative wording that is not evidence-based.

Do not apply these as blind word bans. Preserve standard disciplinary usage and
choose the clearest construction for the actual rhetorical function.

### Claim-strength and hedging gate

Flag unsupported certainty markers such as:

- `clearly`, `obviously`, `certainly`, `undoubtedly`, `definitely`, `absolutely`;
- categorical `always`, `never`, `every`, or `all` where the evidence is bounded;
- `prove`, `demonstrate`, or equivalent causal language when the evidence only
  supports association or interpretation.

Prefer evidence-matched devices where appropriate, including:

- verbs: `suggest`, `indicate`, `imply`, `appear`, `seem`, `tend`;
- modals: `may`, `might`, `could`, and context-appropriate `can`;
- bounded qualifiers such as `primarily`, `generally`, `likely`, `possible`, or
  `consistent with`.

Do not add hedging mechanically. Direct measurements and established procedural
facts should remain direct when uncertainty is not present.

## Stage 4 — Authorship and information-density audit

The goal is not to make academic writing informal. The goal is to make the prose
traceable to the researcher's actual evidence and reasoning.

Flag paragraphs that rely heavily on:

- generic significance statements that could fit many unrelated studies;
- repeated structures such as `These findings suggest that...`;
- stock transitions such as repeated `Moreover`, `Furthermore`, `In addition`,
  `Taken together`, `Notably`, or `Interestingly`;
- highly uniform sentence lengths or repeated grammatical frames;
- vague nouns such as `findings`, `mechanisms`, `interactions`, or `implications`
  where the actual observation can be named;
- polished but low-information summary language;
- paragraphs that state an interpretation without identifying the observations
  that support it.

Prefer the pattern:

`specific observation(s) -> relationship among evidence -> bounded interpretation`

Increase research specificity by naming the relevant condition, comparison,
measurement, temporal pattern, or converging evidence when that information is
already supported by the source text.

## Stage 5 — AI-writing risk classification

Run this stage automatically for every substantive academic-prose revision covered by this workflow.

Do not report an invented probability or percentage of AI authorship. Use a qualitative formulaic-writing risk classification instead:

| Level | Interpretation | Default action |
| --- | --- | --- |
| A | research-specific, natural academic prose | keep |
| B | minor formulaic wording | optional edit |
| C | noticeable repetition or generic framing | revise selectively |
| D | strongly formulaic, over-smoothed, or low-specificity prose | priority rewrite |
| E | pervasive template structure with weak author-specific reasoning | deep restructure |

The automatic audit should check at minimum:

- repeated discourse markers and stock transitions;
- repeated sentence frames or paragraph templates;
- generic significance claims not anchored to the actual experiment;
- excessive symmetry or over-smoothed prose;
- vague evidence references (`these findings`, `this mechanism`) where specific observations are available;
- unnecessary restatement of the same conclusion;
- abrupt shifts in author voice or information density;
- suspiciously generic phrasing that could apply to unrelated studies.

AI-detector outputs, including institutional detector reports, are external
signals only. They must not be treated as proof of authorship and must not
supersede scientific or academic-writing requirements. If an actual detector result is supplied or explicitly requested through an available external service, record the detector name/version/date when known and treat its score only as an auxiliary review signal.

## Stage 6 — Evidence-preserving rewrite

For each revised paragraph:

1. retain the locked scientific content;
2. remove only genuine style, clarity, repetition, or authorship problems;
3. strengthen specificity using information already supported by the document;
4. vary sentence architecture only where it improves clarity or emphasis;
5. keep disciplinary terminology stable;
6. preserve the original evidence boundary and uncertainty level.

Avoid thesaurus-style synonym replacement, random sentence inversion,
intentional grammatical errors, artificial burstiness, or any other tactic whose
sole purpose is to bypass an AI detector.

## Stage 7 — Meaning-diff validation

Compare original and revised versions and explicitly check:

- claim strength unchanged unless separately approved by `PR-RSCH`;
- numerical and experimental meaning unchanged;
- causal direction unchanged;
- species attribution unchanged;
- citations still support the same proposition;
- no new mechanism or conclusion introduced;
- no limitation or alternative explanation removed accidentally.

If any item changes, record it as a substantive scientific revision rather than
an authorship/style edit.

## Recommended audit output

Use a table with at least:

| Section | Paragraph | Scientific status | PolyU style | Authorship risk | Main trigger | Action |
| --- | --- | --- | --- | --- | --- | --- |

For changed high-risk paragraphs, provide:

- the exact problem;
- the evidence that must remain locked;
- the revised wording;
- a short meaning-diff note.

For quantitative issues, distinguish explicitly among **confirmed conflict**,
**apparent discrepancy**, and **needs source-data verification**; do not collapse
all three into a high-severity inconsistency label.

For file-producing tasks, also report the original-safe editing status:

| Original | Revised / branch | Original preserved? | Rollback path |
| --- | --- | --- | --- |

## Completion criteria

- Scientific validity takes precedence over detector-related goals.
- PR-AUTH was triggered automatically for substantive academic-prose changes.
- PolyU / local academic-style constraints have been checked where applicable.
- Formulaic-writing risk is reported qualitatively, not as a fabricated AI
  probability.
- Revised prose is more specific to the actual study rather than merely more
  lexically varied.
- Every substantive wording change passes the meaning-diff validation.
- Quantitative conflict labels have passed the same-basis and derived-metric
  checks before severity is assigned.
- External AI-detector results, if supplied, are treated only as locations for
  additional review rather than as definitive evidence.
- The original document/file remains recoverable through an untouched original, a versioned revised copy, or verified version-control history.
