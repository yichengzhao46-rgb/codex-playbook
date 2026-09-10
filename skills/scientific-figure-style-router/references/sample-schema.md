# Scientific Figure Style Sample Schema

## Purpose

Use one structured record per reference figure or independently useful panel. The database is intended for retrieval and design learning, not for storing unlabeled image files.

A record should make it possible to answer:

- what scientific job the figure performs;
- how the information is composed;
- which visual language it uses;
- which elements are reusable;
- what should not be copied or reused;
- why the figure works for its intended scientific purpose.

## Canonical record

```yaml
sample_id: ""
status: candidate | active | rejected | archived

source:
  journal: ""
  year: null
  article_title: ""
  doi_or_url: ""
  figure_id: ""
  panel_id: ""
  source_checked_at: "YYYY-MM-DD"
  access_note: ""
  rights_or_license: ""
  local_asset_reference: ""  # optional; never assume publisher reuse rights

classification:
  primary_purpose: conceptual_overview | microbial_interaction | mechanistic_pathway | metabolic_pathway | electron_transfer | material_microbe_interface | environmental_process | experimental_design | comparative_perturbation | integrated_mechanism | graphical_abstract | multiscale_zoom
  secondary_purposes: []
  style_family: flat_2d_mechanism | soft_2_5d_schematic | pathway_cutaway_2d | editorial_2d_overview
  dimensionality: 2d | light_2_5d
  layout: linear_flow | two_organism_interaction | central_hub | mirrored_comparison | zoom_in_multiscale | circular_pathway | layered_gradient | evidence_to_model | other
  information_density: low | medium | high
  target_medium: paper | graphical_abstract | presentation | proposal | protocol | other

domain:
  primary_domain: ""
  scientific_entities: []
  process_keywords: []

visual_language:
  cell_style: ""
  material_style: ""
  molecule_style: ""
  arrow_style: ""
  palette: ""
  outline: ""
  shading_or_texture: ""
  background: ""
  text_density: low | medium | high
  label_hierarchy: ""
  panel_or_zoom_style: ""
  negative_space: ""

evidence_semantics:
  evidence_coding_present: yes | no | unclear
  supported_pathway_encoding: ""
  candidate_pathway_encoding: ""
  contextual_pathway_encoding: ""
  causal_language_risk: low | medium | high
  notes: ""

reusability:
  best_reusable_elements: []
  best_reusable_layout_principles: []
  best_reusable_arrow_principles: []
  suitable_for: []
  not_suitable_for: []
  transferable_without_copying: ""

assessment:
  why_it_works: ""
  main_weakness: ""
  scientific_clarity_score: 1-5
  layout_transferability_score: 1-5
  element_reusability_score: 1-5
  style_relevance_score: 1-5
  active_corpus_decision: ""

notes: ""
```

## Required fields for active-corpus admission

The following fields must not be blank when `status: active`:

- `source.journal`;
- `source.year`;
- `source.article_title`;
- `source.doi_or_url`;
- `source.figure_id`;
- `source.rights_or_license` or a note that rights were not verified and no image asset is stored;
- `classification.primary_purpose`;
- `classification.style_family`;
- `classification.dimensionality`;
- `classification.layout`;
- `classification.information_density`;
- `visual_language.arrow_style`;
- `visual_language.palette`;
- `visual_language.text_density`;
- `reusability.best_reusable_elements` or `reusability.best_reusable_layout_principles`;
- `reusability.suitable_for`;
- `reusability.not_suitable_for`;
- `assessment.why_it_works`.

## Annotation rules

### Purpose before journal

Classify what the figure is doing before recording what journal it came from. A visually similar diagram may serve very different scientific functions.

### Panel-level records are allowed

If one multipanel figure contains a uniquely valuable schematic panel, annotate that panel separately. Record both `figure_id` and `panel_id`.

### Record limitations

Every active sample must include at least one `not_suitable_for` or `main_weakness` note. This prevents prestige bias and blind style transfer.

### Separate style from evidence

A dashed line may be visually attractive but could mean different things in different papers. Record the original use and then separately record the reusable semantic principle. Do not assume line style has a universal meaning across source papers.

### Prefer transferable observations

Good observations:

- “balanced two-organism layout leaves a central exchange zone”;
- “material texture is shallow and does not compete with electron-flow arrows”;
- “one saturated accent is reserved for the focal route”;
- “candidate links are visually weaker than experimentally supported links.”

Weak observations:

- “looks like Nature”;
- “high-end style”;
- “beautiful colors.”

## Suggested corpus queries

The router should be able to retrieve records using combinations such as:

- `microbial_interaction + flat_2d_mechanism + two_organism_interaction`;
- `material_microbe_interface + soft_2_5d_schematic + zoom_in_multiscale`;
- `comparative_perturbation + mirrored_comparison`;
- `electron_transfer + pathway_cutaway_2d`;
- `graphical_abstract + editorial_2d_overview + low density`.

Journal, year, and domain keywords should refine retrieval after functional matching, not replace it.

## Copyright/provenance note

This schema is deliberately usable without storing the source image. A metadata record plus source link and derived design observations is sufficient for many routing tasks. If an image asset is stored elsewhere, record its rights/license and local reference explicitly.
