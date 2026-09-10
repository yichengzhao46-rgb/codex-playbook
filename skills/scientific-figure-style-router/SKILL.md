---
name: scientific-figure-style-router
purpose: Route environmental microbiology and environmental engineering figure requests by scientific purpose, information type, layout, visual style family, reusable elements, and evidence semantics before drafting or generating the figure.
primary_route: ChatGPT
primary_pr_class: PR-OPS
secondary_validation_lenses:
  - PR-FIG
status: experimental
version: 0.1
validation_status: specification-complete; forward validation pending
---

# 2D/2.5D Scientific Figure Style & Element Router

## Purpose

Use this Skill to turn a scientific drawing request into a repeatable visual-design decision rather than starting from a journal name or an ad hoc image prompt.

The canonical decision chain is:

`Task → figure purpose → information type → evidence semantics → layout → style family → reusable elements → visual language → generation brief → final figure`

The Skill is optimized for environmental microbiology and environmental engineering, especially microbial interactions, methane oxidation, inorganic-carbon assimilation, diffusible metabolite exchange, oxygen perturbation, EET/EEU, microbial–mineral interfaces, semiconductor biohybrids, GAC-facilitated interspecies electron transfer, and potential DIET.

It is not a generic art-style imitation system and must not reduce figure design to “make it look like Journal X.” Journals are reference-source families, not style labels.

## Automatic trigger

Trigger this Skill when the user asks to design, generate, redraw, restyle, plan, or critique a scientific schematic whose main object is one or more of:

- conceptual overview;
- microbial interaction schematic;
- mechanistic pathway;
- metabolic pathway;
- electron-transfer mechanism;
- material–microbe interface;
- environmental-process schematic;
- experimental-design schematic;
- comparative perturbation schematic;
- integrated mechanism model;
- graphical abstract / TOC graphic;
- multiscale or zoom-in scientific schematic.

Also trigger when the user asks which visual style, layout, arrow language, element design, or publication-figure reference family is most appropriate for a scientific concept.

## Do not trigger

Do not use this Skill for:

- ordinary quantitative plots where the main problem is data visualization rather than scientific illustration;
- simple image cleanup, crop, background removal, resolution increase, or isolated raster editing when the design language is already fixed;
- decorative cover art or photorealistic scientific imagery;
- realistic 3D molecular/cellular rendering unless the user explicitly overrides the default 2D/2.5D constraint;
- a figure whose layout/style has already been fully specified and only mechanical execution remains.

For a plot or quantitative figure, route to the normal figure/data workflow. For an isolated element edit, preserve the approved element identity unless the user requests a style redesign.

## Default visual doctrine

Unless the user explicitly requests otherwise:

1. prefer **2D or restrained 2.5D**, never glossy photorealistic 3D;
2. use low-saturation, publication-oriented palettes;
3. use minimal or no drop shadow;
4. keep outlines controlled and consistent;
5. prioritize scientific hierarchy over decorative detail;
6. use white or transparent backgrounds for standalone elements and publication schematics unless environmental context is functionally needed;
7. preserve a stable visual identity for recurring research entities across figures;
8. keep evidence strength and process type visually distinguishable;
9. avoid using journal identity as the only routing criterion;
10. design for grayscale legibility and color-vision accessibility where practical.

## Figure-purpose taxonomy

Classify the requested figure into one primary purpose and optional secondary purposes.

| Purpose | Primary question answered | Typical visual priority |
| --- | --- | --- |
| `conceptual_overview` | What is the high-level research idea? | hierarchy, story flow, low-to-medium density |
| `microbial_interaction` | Who interacts with whom and through what resources? | organism identity, directional exchange, spatial relationship |
| `mechanistic_pathway` | What causal/process chain is proposed? | pathway order, evidence status, causal boundaries |
| `metabolic_pathway` | How do substrates/intermediates/pathways connect? | biochemical direction, compartment/pathway separation |
| `electron_transfer` | Where do electrons originate, travel, and terminate? | electron identity, donor/acceptor distinction, conductive/soluble route |
| `material_microbe_interface` | How does a cell interact with a mineral/material surface? | interface geometry, contact, surface process, 2.5D depth cue |
| `environmental_process` | How does a process operate across an environmental gradient or habitat? | spatial layers, gradients, source/sink, ecological context |
| `experimental_design` | What was manipulated and measured? | groups, sequence, controls, readouts |
| `comparative_perturbation` | What changes between two or more controlled conditions? | mirrored layout, visual equivalence, one-variable contrast |
| `integrated_mechanism` | How do multiple evidence streams converge on one model? | evidence-to-model hierarchy, supported vs candidate links |
| `graphical_abstract` | What is the paper’s single take-home story? | editorial simplification, strong focal path, minimal text |
| `multiscale_zoom` | How do system, interface, and molecular/cellular views connect? | nested scale, callout/zoom, cross-scale continuity |

If more than two purposes are equally dominant, first simplify the scientific message. Do not solve an unclear story by adding more icons.

## Style-family taxonomy

Use one dominant style family per figure. Hybridization is allowed only when functionally useful.

### 1. Flat 2D mechanism

Best for:

- microbial interactions;
- diffusible metabolite exchange;
- integrated mechanism figures;
- environmental microbiology process models;
- paper figures with medium information density.

Characteristics:

- flat or nearly flat cells/icons;
- restrained outlines;
- limited texture;
- direct arrows and compact labels;
- visual emphasis from spacing and hierarchy rather than shading.

Reference-source language often overlaps with ISME Journal, Nature Microbiology, Nature Communications, ES&T, and Water Research mechanism schematics.

### 2. Soft 2.5D schematic

Best for:

- mineral–microbe interfaces;
- GAC;
- Se nanoparticles;
- electrodes;
- semiconductor biohybrids;
- conductive interfaces and surface electron exchange.

Characteristics:

- simple depth cue or shallow perspective;
- restrained surface texture;
- minimal soft shading only where needed to separate material/cell/interface;
- no glossy rendering, cinematic lighting, or realistic 3D scene construction.

Reference-source language often overlaps with EES and Nature Communications interface/biohybrid figures.

### 3. 2D pathway / cutaway

Best for:

- membrane transport;
- respiratory chain;
- intracellular metabolic pathways;
- EET/EEU route depiction;
- cell-envelope cutaways.

Characteristics:

- simplified membrane or compartment cross-section;
- pathway modules separated spatially;
- electron/carbon/metabolite arrows use distinct semantics;
- molecular detail is included only when it carries mechanistic meaning.

### 4. Editorial 2D overview

Best for:

- presentation opening slides;
- objective overview;
- graphical abstract;
- high-level conceptual framing;
- science-story summary.

Characteristics:

- fewer elements;
- stronger compositional hierarchy;
- larger negative space;
- short labels;
- one dominant reading path;
- polished but not decorative.

## Layout taxonomy

Choose the layout from the scientific relationship before choosing the art style.

| Layout | Use when | Default reading logic |
| --- | --- | --- |
| `linear_flow` | sequential process or experiment | left→right or top→bottom |
| `two_organism_interaction` | defined coculture or donor–partner system | organism A ↔ central exchange space ↔ organism B |
| `central_hub` | one material/metabolite/interface connects several routes | inputs → hub → outputs |
| `mirrored_comparison` | 5% vs 25% O2, treatment vs control | matched left/right scenes with one controlled contrast |
| `zoom_in_multiscale` | habitat→cell→membrane/material interface | overview + callout + detailed inset |
| `circular_pathway` | cycle/regeneration is the scientific point | circular process with clear entry/exit |
| `layered_gradient` | oxic–anoxic, depth, redox, habitat stratification | stacked spatial zones with directional gradients |
| `evidence_to_model` | several measurements support an integrated mechanism | evidence modules → bounded model |

Avoid circular layouts for processes that are not biologically cyclic. Avoid mirrored comparison if the panels differ in several unrelated variables.

## Information-density bands

Assign one band before drafting:

- `low`: one message, typically 3–7 primary objects;
- `medium`: one main pathway plus secondary context;
- `high`: multiple mechanistic modules, compartments, or evidence classes.

A graphical abstract should normally remain `low` or `medium`. A final integrated mechanism figure may be `medium` or `high`, but the reader must still be able to identify the primary path within seconds.

## Reference-source families

Use source journals to learn reusable visual decisions, not to clone figures.

Default source priorities for this research profile:

- **The ISME Journal** — microbial interaction, ecological mechanism, cross-feeding, defined-community schematics;
- **Nature Microbiology** — high-level microbial mechanism and conceptual framing;
- **Nature Communications** — integrated mechanism, multiscale/cellular schematics, interface figures;
- **Environmental Science & Technology** — environmental process and graphical-summary language;
- **Water Research** — experimental systems, treatment/perturbation comparisons, environmental-engineering mechanism;
- **Science Advances** — high-level scientific storytelling;
- **Energy & Environmental Science** — biohybrid, electron-flow, material–microbe interface;
- **Nature Water** — environmental-process and engineering-system visual language.

For the default corpus, emphasize ISME Journal, ES&T, Water Research, and Nature Communications. Do not let one journal family dominate every purpose category.

## Reusable element library

The library should represent elements as reusable visual identities rather than one-off images.

Core element categories:

- cell morphology: cocci, rods, aggregates;
- named research organisms;
- membranes and cell-envelope cutaways;
- mineral particles;
- GAC;
- Se nanoparticles;
- semiconductor/mineral interfaces;
- electrode;
- gas molecules;
- metabolites;
- chemical structures;
- electron symbols;
- arrows/connectors;
- inhibition symbols;
- oxic–anoxic or redox gradients;
- environmental backgrounds;
- zoom-in/callout frames;
- labels, font hierarchy, panel tags.

### Project visual-identity tokens

For recurring user research, preserve stable identities across figures even when the style family changes:

- **Bath**: spherical methanotroph identity; default cool/blue family;
- **RP**: rod-shaped partner identity; default restrained red/warm family;
- **CH4, O2, CO2/HCO3-**: consistent gas/carbon symbols;
- **H2, formate, acetate, riboflavin-like mediator**: consistent metabolite/transfer identities;
- **electron**: consistent `e−` identity and electron-flow arrow language;
- **GAC, Se, mineral/semiconductor, electrode**: stable material identities.

A style-family switch may change rendering depth, texture, and outline treatment, but should not silently change the identity of the same scientific entity.

## Arrow and line semantics

Arrows are scientific notation, not decoration.

Every connector must have both:

1. a **process role**; and
2. an **evidence state**.

### Process roles

Use explicit classes:

- `metabolic_flow`;
- `electron_flow`;
- `carbon_flow`;
- `causal_relationship`;
- `bidirectional_exchange`;
- `inhibition`;
- `material_contact_or_interface` where a connector represents contact rather than transport.

### Evidence states

Use explicit classes:

- `supported` — supported by the evidence level appropriate to the figure;
- `candidate` — plausible/proposed but unresolved;
- `contextual` — literature/contextual pathway shown for orientation rather than established in the current experiment.

Do not encode process role and evidence state using the same visual variable. Example: arrowhead/direction and label can encode process role, while solid/dashed line pattern encodes evidence state. Color can reinforce meaning but must not be the only distinction.

### Default connector logic

- solid directional line: supported process link;
- dashed directional line: candidate/hypothetical link;
- double-headed arrow: genuine bidirectional exchange only;
- T-bar or explicit inhibitory symbol: inhibition;
- electron flow: visibly distinct `e−` label and/or arrow family;
- carbon flow: label the carbon-containing species or carbon route when ambiguity is possible;
- causality: do not use causal-style arrows when the evidence only shows association.

Avoid decorative curved arrows that imply cycles or feedback without biological justification.

## Evidence-aware figure design

A polished figure must not strengthen the scientific claim beyond the underlying evidence.

Before finalizing a mechanism figure, classify each major edge as one of:

- directly observed / experimentally isolated;
- supported by converging evidence;
- candidate / mechanistically plausible;
- contextual only.

Use visual strength consistently with those classes.

For Bath–RP work in particular:

- community-level EA-IRMS must not be drawn as direct species-resolved RP isotope incorporation;
- community ATP/NAD(H) must not be visually assigned to RP without species-resolved evidence;
- transcript presence/expression must not be drawn as direct metabolite flux;
- absence of a Bath-only transcriptomic comparator means no Bath induction/upregulation arrow or label;
- H2/formate/acetate/riboflavin-like routes should remain individually bounded unless route-specific evidence resolves them;
- GAC-associated enhancement alone does not visually become proven DIET.

The figure may still communicate a strong integrated model when multiple evidence streams converge; unresolved steps should be visually bounded rather than erased.

## Style database record requirement

Every reference sample used for learning or routing should have a structured metadata record. The canonical schema is in [`references/sample-schema.md`](references/sample-schema.md).

Minimum fields include:

- source journal/year/article/figure/panel;
- source identifier or link;
- rights/provenance note;
- figure purpose;
- style family;
- dimensionality;
- layout;
- information density;
- cell/material/arrow style;
- palette/outline/background/text density;
- evidence coding;
- best reusable elements;
- suitable / not suitable uses;
- why the figure works.

Do not maintain the library as an unlabeled folder of JPG/PNG files.

## Copyright and source-image policy

The playbook should store **methods, metadata, schemas, and derived style observations**, not a bulk mirror of publisher figures.

Default rules:

- store citation/source metadata and structured visual observations;
- do not commit full publisher figures merely for style reference unless reuse rights clearly permit it;
- keep any licensed/open-access image assets in the appropriate execution/library location with rights information;
- do not trace or reproduce a published figure so closely that the new figure becomes a derivative copy of its composition or artwork;
- learn principles and elements across multiple references rather than cloning one source.

## Style Router procedure

### Step 1 — Define the scientific message

Extract:

- main scientific question;
- direct observation vs interpretation vs hypothesis;
- target output: paper, presentation, graphical abstract, proposal, protocol;
- primary audience;
- essential entities and processes;
- scientific relationships that must not be implied.

If the user already supplied this information, do not ask again.

### Step 2 — Assign the figure purpose

Choose one primary purpose from the taxonomy and at most two secondary purposes.

### Step 3 — Set information density

Choose `low`, `medium`, or `high` and identify what must be omitted from the main frame or moved into an inset/secondary panel.

### Step 4 — Choose the layout

Choose the layout from the relationship structure, not from aesthetics.

### Step 5 — Choose the style family

Map purpose + material/spatial needs to one dominant style family.

### Step 6 — Retrieve reference patterns

Search the style database by:

`purpose + layout + style family + information density + scientific domain + required elements`

Use several reference samples when possible. Prefer learning a recurring pattern over copying an outlier.

### Step 7 — Assemble reusable elements

Select stable organism/material/metabolite identities from the element library. Create new element identities only when the existing vocabulary cannot express the science cleanly.

### Step 8 — Assign connector/evidence semantics

For every important arrow or connector, assign process role + evidence state before drawing.

### Step 9 — Produce a Figure Design Card

Before generation, internally or explicitly when useful, produce:

```text
Target medium:
Primary figure purpose:
Secondary purpose(s):
Scientific take-home message:
Information density:
Layout:
Style family:
Dimensionality:
Reference-source language:
Key reusable elements:
Process-flow semantics:
Evidence-state semantics:
Palette/outline/background:
Text-density rule:
Zoom/inset strategy:
Must show:
Must not imply:
Generation/editing brief:
```

### Step 10 — Generate or hand off

Use the Figure Design Card as the authoritative design brief. The image-generation tool or external illustrator should not independently reinterpret the evidence hierarchy.

### Step 11 — QA the result

Check:

- scientific identities are correct;
- layout matches the intended reading path;
- arrow direction and evidence coding are correct;
- one dominant message is visible;
- text does not replace the visual logic;
- no unwanted photorealistic/3D styling was introduced;
- Bath/RP/material identities remain consistent with the library;
- colors, outlines, and label hierarchy are coherent;
- candidate links do not visually appear stronger than supported links;
- the figure remains legible at intended final size.

## Default routing examples

### Bath–RP final mechanism figure

Route as:

`paper figure → integrated mechanism + microbial interaction → medium/high density → two-organism interaction / evidence-to-model → flat 2D mechanism → ISME/Nature Communications visual language`

Default composition: Bath on one side, RP on the other, diffusible transfer space between them, clear methane upstream input, recipient energy/redox/CBB module downstream, supported and candidate links distinguished.

### Bath–Se biohybrid hypothesis

Route as:

`material–microbe interface + electron transfer → medium density → zoom-in multiscale → soft 2.5D schematic → EES/Nature Communications visual language`

Default composition: Bath cell + restrained Se/mineral interface, light/photoelectron cue if scientifically required, shallow depth, local interface zoom, electron path distinct from methane/carbon path.

### 5% versus 25% O2 perturbation

Route as:

`comparative perturbation → medium density → mirrored comparison → flat 2D mechanism or editorial 2D → Water Research/ES&T/Nature Communications visual language`

The two scenes should remain compositionally matched so oxygen availability is the dominant visible change.

### GAC-facilitated interspecies electron coupling

Route as:

`material–microbe interface + electron transfer + microbial interaction → medium density → two-organism + central hub → soft 2.5D/flat hybrid`

Keep direct conductive/electron-transfer interpretation visually separate from alternative soluble transfer routes unless experimentally resolved.

## Corpus-building workflow

Build the database incrementally:

1. discover candidate figures from the source-journal families;
2. verify source/provenance and whether the figure is actually useful for visual learning;
3. annotate each sample using the schema;
4. extract reusable design principles and element patterns;
5. tag the sample by purpose/style/layout, not just journal;
6. reject samples that are visually attractive but scientifically unsuitable for the target use;
7. periodically check balance across purpose/style/layout categories;
8. validate the router on real user requests;
9. revise taxonomy only when repeated cases expose a real gap.

Do not add samples merely to increase corpus size. Coverage diversity and transferability matter more than raw count.

## Corpus quality gate

A sample is eligible for the active corpus only when:

- its source is identifiable;
- its figure purpose can be classified;
- its layout/style can be described without relying only on journal identity;
- at least one reusable design principle or element can be articulated;
- its limitations/not-suitable cases are recorded;
- it is not retained only because the journal is prestigious.

A style category should not be treated as mature from one or two visually similar examples.

## Validation plan

The Skill remains **experimental** until it is forward-validated in `codex-workbench` or equivalent real use.

Minimum validation set should include materially different requests:

1. Bath–RP final integrated mechanism figure;
2. Bath–Se material–microbe biohybrid hypothesis;
3. 5% vs 25% O2 mirrored perturbation;
4. GAC-facilitated interspecies electron-transfer concept;
5. intracellular/membrane EET cutaway;
6. environmental oxic–anoxic gradient overview;
7. graphical abstract version of one of the above;
8. negative control: a simple quantitative line plot that should not trigger this Skill.

Evaluate whether the router correctly selects purpose, layout, style family, element identity, and evidence-arrow semantics without forcing every request into one house style.

## Acceptance criteria for promotion

Promote beyond experimental only when real-task validation shows that:

- figure-purpose classification is reliable across several request types;
- style-family selection changes appropriately with scientific function;
- layout routing is not reduced to journal imitation;
- Bath/RP and recurring material identities remain visually consistent;
- arrow semantics correctly distinguish process role and evidence state;
- 2D/2.5D defaults prevent unwanted glossy 3D rendering;
- generated figures become more consistent and require fewer repeated style corrections;
- the corpus metadata are useful for retrieval rather than decorative cataloguing;
- at least one negative control confirms the Skill is not over-triggered.

## Relationship to PR routing

Changes to this Skill, its taxonomy, schema, or routing logic are normally `PR-OPS`, because the authoritative object is a reusable operating method.

Use `PR-FIG` as the secondary validation lens for scientific visual semantics, layout, arrow meaning, visual hierarchy, and publication suitability.

Using this Skill to create one concrete manuscript schematic does **not** make that figure task `PR-OPS`; the actual figure remains a `PR-FIG` task.

## Maturity

Status: **experimental / specification-complete**.

This version defines the routing architecture, taxonomy, sample metadata, evidence-aware arrow logic, project visual identity, and validation plan. It does not claim that a large top-journal style corpus has already been populated or that the router has been forward-validated on generated figures.
