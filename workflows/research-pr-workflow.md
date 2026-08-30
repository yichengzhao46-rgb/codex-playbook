# Research PR Workflow

Use this workflow to package changes to research methods, literature systems,
data pipelines, figures, Origin projects, documents, and Codex operating rules.
It extends the repository's general [Pull Request Workflow](pull-request-workflow.md).

## Entry conditions

1. Start from actual changed files or an explicit proposed change set.
2. Apply the [Research PR Routing Rules](../rules/research-pr-routing.md).
3. Select one project key (or `GENERAL`) and one primary PR class.
4. Complete specialist execution before returning here for PR packaging.
5. For reusable `PR-OPS` design or material restructuring, first apply the [External Workflow Benchmark and Local Adaptation](external-workflow-benchmark.md) workflow unless its non-trigger conditions apply.
6. Create a Draft PR by default and leave merge approval to a human.

## Procedure

1. Build a compact change inventory:
   - changed files
   - user-facing behavior change
   - affected workflow, agent, script, or output
   - validation performed and result
   - rollback path when relevant
2. Identify the authoritative source and the matching validation gate below.
3. Separate what changed from what was verified. Do not imply that visual,
   source-data, Zotero storage, Word render, or editable-project QA passed unless
   that check was performed.
4. Review the local diff for unrelated files, credentials, private data, and
   accidental generated output.
5. Draft the PR with the [Research PR Template](../templates/research-pr-template.md).
6. Push the task branch and create a Draft PR.

## Validation gates by class

### `PR-OPS`: skills, agents, tools, and routing

- Source of truth: changed skill, agent, rule, template, configuration, or
  installed copy.
- Check trigger scope, frontmatter or metadata, duplicated routers, placeholder
  text, and source-versus-installed status.
- Run the relevant structural validator when available.
- For project-agent routing, preserve one coordinator plus one primary
  specialist and staged context loading.
- When the change designs, materially restructures, or promotes reusable operating behavior, apply the external benchmark/local-adaptation gate before implementation.
- Do not copy external workflow architecture directly. Record which principles were adopted, adapted, rejected, or left unresolved, and tie accepted changes to a concrete local need or user-experience signal.
- For meaningful new trigger/routing behavior, require at least one positive case and one negative control before stable promotion.

### `PR-LIT`: Zotero and literature systems

- Check title, authors, DOI, parent-child attachments, physical storage,
  duplicates, collection/tag placement, and index state as applicable.
- Do not treat attachment metadata as proof that the file exists.
- Separate strict evidence, near matches, and unresolved uncertainty.

### `PR-RSCH`: manuscripts, chapters, and academic writing

- Check the target objective or rhetorical function, claim-evidence alignment,
  direct versus analogy evidence, terminology, and unresolved controls.
- For Bath-RP/MOB-EET work, do not overstate Bath EEU, partner DIET,
  species-specific flux, or causal donor transfer without direct tests.
- For ELC work, check the local prompt, rubric, handout, and sample conventions.
- When authorship, academic style, or AI-writing risk is in scope, apply the
  [PR-AUTH Academic Authorship and AI-Writing Risk Workflow](pr-auth-academic-writing.md)
  as a specialist checklist under `PR-RSCH`; do not create a separate PR class.
- In PR-AUTH work, scientific validity and evidence boundaries take precedence
  over institutional style, author-specific voice, and detector-related goals.

### `PR-DATA`: data processing and statistics

- Check files, sheets, columns, units, groups, missing values, replicate
  structure, formulas, tests, sidedness, pairing, corrections, and targets.
- Validate with a deterministic rerun or checked calculation table.
- For EEM/FRI or calibration work, also check metadata rows, wavelength bounds,
  scatter masking, slit/bandwidth matching, calibration basis, and sample count.

### `PR-FIG`: academic figures and local figure edits

- Prefer the source in this order: script/project, source table, vector file,
  then raster image.
- Record changed layers, statistics/annotation basis, preview, and final export.
- For raster-local edits, state whether unchanged pixels were preserved.
- Distinguish visual QA from source/export QA.

### `PR-ORG`: Origin-native deliverables

- Verify that the editable `.opju` contains native workbook and graph pages.
- Check source-table synchronization and preview export.
- A pasted image is not an editable Origin-native deliverable unless explicitly
  requested.

### `PR-DOC`: Word and PDF workflows

- Distinguish direct text/structure extraction from layout/render QA.
- Check comments or tracked-change structure when relevant.
- Render Word deliverables to PDF or PNG for visual inspection when possible;
  state clearly when render QA is blocked.

### `PR-MIX`: inseparable multi-object changes

Use `PR-MIX` only when one atomic change spans multiple authoritative objects and
splitting the change would make one or more parts unusable.

- Name every authoritative object and every constituent PR class.
- Explain why the change cannot be split into independent PRs.
- Apply the union of all validation gates required by the constituent classes.
- Record validation results separately by class or object.
- Document shared and class-specific rollback implications.
- Do not use `PR-MIX` to bypass a failed or inconvenient class-specific check.

## Evidence boundaries

For research-supporting changes, keep these categories separate in the PR:

- directly verified
- source-backed but not reproduced
- inferred or transferred by analogy
- not checked or unresolved

## Completion criteria

- The project key (or `GENERAL`) and primary PR class are stated.
- The authoritative source and validation level are explicit.
- For `PR-MIX`, constituent classes and the reason splitting is not viable are stated.
- For benchmark-triggered `PR-OPS` work, external patterns and local adaptation decisions are documented at the level needed to justify the design without turning the stable workflow into a literature review.
- The final diff contains no unrelated changes or secrets.
- Known limitations and rollback are documented.
- The Draft PR is open and not merged automatically.
