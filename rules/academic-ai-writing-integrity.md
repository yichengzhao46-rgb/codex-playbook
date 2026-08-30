# Academic AI-Writing Integrity Rule

Use this rule with the existing `PR-AUTH` workflow under `PR-RSCH` when AI-assisted, AI-edited, detector-flagged, or substantively revised academic writing is being reviewed.

This rule governs **integrity, authorial control, and reversible editing**, not detector evasion. The detailed review procedure remains in [`../workflows/pr-auth-academic-writing.md`](../workflows/pr-auth-academic-writing.md).

## Core principle

Scientific validity, evidence boundaries, disciplinary writing quality, human-author control, and recoverability of the original take precedence over any AI-detector score or stylistic attempt to appear human-written.

Do not rewrite text solely to reduce an AI-detector score, hide AI assistance, or imitate arbitrary human-writing irregularities.

## Original-safe editing gate

For substantive manuscript or academic-document edits, do not overwrite the only recoverable original.

Use the first practical option below:

1. keep the original untouched and create a clearly versioned revised copy;
2. for repository text, edit on a dedicated version-controlled branch so the pre-edit version remains recoverable;
3. if in-place editing is genuinely required, verify a backup before overwrite.

For Word/PDF deliverables, prefer `original + revised copy` over silent in-place replacement. If tracked changes are used, the original should still remain separately recoverable.

If no reliable recovery path exists, stop before destructive overwrite and report the constraint.

Record the recovery path when producing a revised file or meaningful repository change.

## Detector interpretation

- Treat detector output as a screening signal only.
- Do not interpret a detector percentage as the percentage of text actually written by AI.
- Do not define a detector score as a pass/fail threshold for manuscript quality or authorship.
- Do not optimize prose against a detector target.
- Use detector-flagged passages only as locations for closer review of scientific precision, formulaic wording, specificity, evidence alignment, and authorial control.

## Acceptable reasons to revise

Revise when the change improves one or more of the following without weakening scientific accuracy:

- claim-evidence alignment;
- scientific precision;
- clarity and information density;
- disciplinary or institutional academic style;
- terminology consistency;
- paragraph logic and rhetorical economy;
- explicit connection between observations and bounded interpretation;
- author-specific reasoning and traceability to the underlying study.

A lower detector score may occur after such a revision, but it is not itself evidence that the revision is better.

## Humanizer anti-pattern

Reject edits whose main purpose is detector avoidance, including:

- thesaurus-style synonym replacement;
- random sentence inversion or artificial sentence-length variation;
- deliberate grammatical errors or awkwardness;
- removal of valid technical terminology because it appears formulaic;
- weakening, strengthening, or reassigning a scientific claim to change detector output;
- deleting limitations, uncertainty, or alternative explanations to make a narrative appear more natural;
- adding unsupported personal voice, anecdote, or conversational language solely to appear human-written.

## AI-assistance provenance

When provenance materially matters for review, collaboration, institutional policy, or submission, record the highest applicable level without inventing certainty:

- `author-drafted` — substantive prose originated from the author and was not materially restructured by AI;
- `AI-polished` — AI assisted with language, grammar, concision, or local clarity while substantive reasoning remained author-controlled;
- `AI-restructured` — AI materially reorganized paragraphs, argument flow, or synthesis and therefore requires stronger meaning-diff verification;
- `mixed-or-unknown` — provenance cannot be cleanly reconstructed from available evidence.

This record is for transparency and review control. It is not an authorship detector.

Where institutional, journal, funder, or collaborator disclosure rules apply, follow the most specific applicable policy.

## Human-author verification

Before final acceptance of materially AI-assisted academic prose, require human-author verification of substantive content. At minimum confirm that:

- major claims remain intended by the author;
- numerical values, units, groups, time points, and statistical meaning are correct;
- citations still support the propositions they are attached to;
- causal direction and species attribution are unchanged unless explicitly revised;
- uncertainty and limitations were not silently removed;
- no new mechanism, result, or conclusion was introduced without evidence.

For high-risk or heavily restructured passages, preserve a concise meaning-diff note or tracked comparison.

## Relationship to `PR-RSCH`

This rule does not create a separate PR class.

- Academic prose remains `PR-RSCH`.
- Use `PR-DATA` as a secondary validation route when resolving a quantitative discrepancy requires deterministic recalculation or raw-data verification.
- Use `PR-DOC` only when the changed authoritative object is document structure, rendering, tracked changes, pagination, or related native-document behavior.
- Do not use `PR-MIX` merely because a detector, Word file, or data table was consulted during review.

## Completion criteria

A review passes this integrity rule only when:

- detector output has not been treated as authorship proof or a target score;
- revisions have an academic or scientific rationale independent of detector evasion;
- substantive meaning has been preserved or explicitly re-reviewed under `PR-RSCH`;
- AI-assistance provenance is recorded when materially relevant and knowable;
- a human author has verified substantive claims before final acceptance of materially AI-assisted prose;
- the original remains recoverable through an untouched original, versioned revised copy, verified backup, or version-control history.
