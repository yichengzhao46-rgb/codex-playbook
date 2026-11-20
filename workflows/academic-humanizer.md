# Academic Humanizer

Use this final editing pass within [PR-AUTH](pr-auth-academic-writing.md) for an explicit
`academic-humanizer` request or author-voice calibration of near-final academic prose. It applies
to manuscripts, theses, confirmation reports, and rebuttals. For review-only requests, return the
diagnosis in the requested format. For broader research review, use the standard PR-AUTH workflow.

## Inputs

- The passage to review or revise and, when provided, its section and target venue.
- Optional writing samples as pasted text or attached PDFs. Use passages the author wrote or
  published examples they designate as style references.
- The figures, tables, citations, and other supporting material the author has supplied or identified.

## Editing pass

1. **Check the evidence.** Apply PR-AUTH's meaning lock and scientific evidence audit before
   editing. Identify the strength and scope of each claim, including its measured quantity,
   comparison, conditions, organism or population, uncertainty, and evidence pointer. Record any
   unresolved claim or citation question for the author. Apply [PR-CAL](pr-cal-evidence-calibration.md)
   when adjudicating a scientific claim is part of the task.

2. **Read for style.** Read the relevant sections of the supplied samples before rewriting. Prefer
   passages that match the target's article type and section. Use author-written samples to
   calibrate personal voice and author-selected publications to calibrate the requested style.
   Identify useful habits such as sentence rhythm, paragraph openings, transitions, and placement of
   qualifiers. Apply them in fresh wording that fits the section and any applicable venue
   requirements. Draw scientific details solely from the target text and its supporting material. When a
   representative sample is unavailable, use restrained academic English and report that the style
   pass used the target section as its guide.

3. **Make targeted edits.** Replace stock openings, redundant transitions, clause-heavy sentences,
   and vague wording when the revision makes the point clearer. Keep disciplinary terminology and
   evidence-matched qualifiers. Retain every citation, equation, number, unit, and figure or table
   reference, with each citation still supporting the same proposition. Put proposed changes to
   data, interpretation, or citation support in the review notes for author verification. Continue
   with wording edits whose meaning is clear.

4. **Compare with the original.** Apply PR-AUTH's meaning-diff check to the revised passage. Check
   that the same result, comparison, attribution, causal direction, and uncertainty are conveyed
   after splitting or reordering sentences. Check citation placement as well as citation presence.
   Restore the original wording where an edit changes the evidence boundary. Follow the
   [academic AI-writing integrity rule](../rules/academic-ai-writing-integrity.md) for recoverable
   file edits, author verification, and disclosure.

## Output

Return the revised passage in the requested language and a short note on substantive wording
changes and their reasons. Include author verification items when any remain. Apply the requested
markup or tracked-edit convention if one was specified.

A direct invocation in a workspace with this playbook available is:

> Run academic-humanizer on my Discussion. Use the relevant sections of the attached PDFs as
> style references and the supplied figure as evidence. Show the revision and briefly explain
> the consequential wording changes.

## Validation examples

- **Author-sample pass.** The author supplies a near-final Discussion passage and a representative
  sample with short result sentences and a separate sentence for interpretation. Keep a bulk
  isotope result attributed to the whole coculture, retain its figure reference, and keep
  diffusible exchange framed as a possible explanation. The author sample guides sentence
  structure.
- **Published PDF references.** For a research manuscript Discussion with one research article
  and two review samples, use the research article's relevant sections to see how the authors
  connect results, controls, and interpretation. Draw on review sections to frame context or
  synthesize evidence where relevant.
- **Evidence question.** A bulk isotope measurement is cited for species-specific fixation. Flag
  the attribution for review and continue with safe wording changes elsewhere in the passage.
- **Routing control.** A request to recalculate isotope enrichment from a spreadsheet follows
  PR-DATA. A general scientific manuscript review follows PR-RSCH with the relevant PR-AUTH checks.

This workflow is experimental pending use on author-approved manuscript excerpts. Its author-sample
and venue calibration procedure was adapted from
[AIScientists-Dev/academic-humanizer](https://github.com/AIScientists-Dev/academic-humanizer/blob/main/SKILL.md).
