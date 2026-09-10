# Visual Language Specification

## Goal

Define a consistent research visual identity that survives across different figure purposes without forcing every figure into the same rendering style.

The rule is:

> **Scientific identity stays stable; rendering depth and composition may change with figure function.**

## 1. Entity identity system

### Bath

Default identity:

- spherical/coccoid bacterial morphology;
- cool, restrained blue family;
- simple cell envelope;
- no generic rod-cell substitution;
- no unnecessary flagella or organelles unless specifically relevant.

May appear as:

- flat 2D sphere/coccus in microbial-interaction figures;
- light 2.5D sphere at a material interface;
- partial cutaway in membrane/EET figures.

The morphology and primary identity color should remain recognizable across these modes.

### RP

Default identity:

- rod-shaped bacterial morphology;
- restrained warm/red family;
- simple envelope;
- preserve species identity rather than replacing with a generic purple photosynthetic cell trope.

May appear flat, light 2.5D, or as a cutaway when functionally needed.

### Recurring molecular/process identities

Maintain stable tokens for:

- CH4;
- O2;
- CO2 / HCO3−;
- H2;
- formate;
- acetate;
- riboflavin or riboflavin-like soluble mediator when scientifically appropriate;
- e−;
- nitrate/other terminal acceptors when present;
- light/photon cue when required in a biohybrid concept.

Do not turn every molecule into a ball-and-stick rendering. Use chemical structures only when molecular identity itself matters.

### Recurring material identities

Maintain a recognizable family for:

- GAC: irregular porous conductive granule, low-saturation dark neutral/brown;
- Se nanoparticles: restrained warm mineral/yellow-brown family, particulate rather than glossy metallic spheres unless justified;
- generic mineral/semiconductor: low-saturation earth/mineral palette with shallow texture;
- electrode: simplified functional geometry with no unnecessary industrial detail.

## 2. Color doctrine

Color should encode identity and hierarchy, not decoration.

Default rules:

- use a mostly low-saturation palette;
- reserve stronger saturation for focal information only;
- avoid rainbow coding when fewer semantic groups exist;
- keep organism identities stable across figures;
- do not rely on red/green contrast alone;
- verify that key distinctions survive grayscale where practical;
- background should normally remain white, transparent, or very light neutral.

A figure can borrow palette relationships from a reference source, but should not copy a distinctive palette/composition pair from one published figure.

## 3. Outline and shading doctrine

### Flat 2D

- consistent, restrained outlines;
- no strong bevels;
- no glossy highlights;
- little or no shadow;
- use spacing and contrast to separate layers.

### Soft 2.5D

- depth is permitted only to clarify contact, surface, porosity, or interface;
- use one coherent light/depth logic;
- keep shadows soft and shallow;
- avoid cinematic lighting and realistic 3D materials.

### Cutaway

- membrane/compartment boundaries should be visibly distinct;
- internal detail must serve the mechanism;
- avoid anatomical realism that obscures pathway logic.

## 4. Connector grammar

### Direction

- single arrowhead = directional transfer/process;
- two arrowheads = genuine bidirectional exchange;
- no arrowhead = physical association/interface only, unless explicitly labeled otherwise;
- T-bar or inhibition glyph = inhibition/suppression.

### Evidence strength

Default proposal:

- solid connector = supported at the evidence level used by the figure;
- dashed connector = candidate/hypothetical;
- lighter contextual line = literature/context only.

Do not encode both electron-vs-carbon flow and supported-vs-candidate status only with solid/dashed lines. Use independent channels.

### Process identity

Recommended combinations:

| Process | Required semantic cue |
| --- | --- |
| electron flow | `e−` label and distinct electron-flow connector family |
| carbon flow | carbon-containing species/route label when ambiguity exists |
| metabolic product transfer | metabolite label/icon on or adjacent to connector |
| causal relation | explicit cause→effect framing only when evidence supports causality |
| inhibition | T-bar/inhibitory glyph plus concise label if needed |
| material contact | contact/interface cue, not automatically an electron-transfer arrow |

## 5. Text hierarchy

A schematic should not become a paragraph with icons.

Default hierarchy:

1. figure/panel title if needed;
2. organism/material labels;
3. pathway or process labels;
4. metabolite/electron labels;
5. compact evidence annotations only when scientifically necessary.

Use short phrases. Avoid repeating information already obvious from position and iconography.

For paper figures, text density should be lower than the number of conceptual relations would tempt the designer to use. Move explanation to the figure legend when it does not need to be read inside the diagram.

## 6. Composition rules by scientific relationship

### Two-organism exchange

Use:

- stable organism positions;
- an intentional exchange zone between cells;
- upstream substrate at the donor side;
- downstream recipient function near the recipient;
- clear separation of soluble, conductive, and contextual routes.

Avoid crossing arrows through cell bodies when a central exchange lane can carry the same meaning.

### Material–microbe interface

Use:

- material surface/granule as a real spatial object;
- cell positioned at or near the interface;
- contact/electron direction shown locally;
- zoom inset if the interface mechanism needs more detail than the overview can carry.

Avoid floating material icons disconnected from spatial contact when the mechanism depends on interface geometry.

### Comparative perturbation

Keep:

- same object count;
- same organism positions;
- same scale;
- same label hierarchy;
- same base palette.

Change only the intended perturbation and its mechanistically downstream consequences. This makes the comparison scientifically legible rather than merely decorative.

### Evidence-to-model

Place empirical evidence modules outside or upstream of the integrated model. Do not redraw every measurement as if it were itself a mechanistic step.

## 7. Environmental gradients

For oxygen/redox/depth gradients:

- use a directional spatial gradient only when it represents a real environmental axis;
- place organisms/processes in meaningful zones;
- avoid strong atmospheric gradient effects that look decorative;
- label endpoints/conditions rather than every intermediate shade.

A gradient must encode a quantity or condition, not just make the background look sophisticated.

## 8. Zoom-in grammar

A zoom-in inset is appropriate when:

- the overview establishes environmental/system context;
- the inset resolves a cell–material or membrane mechanism;
- the scale transition itself aids understanding.

Use a clear callout box/connector. The inset should add mechanistic resolution, not repeat the same scene at a larger size.

## 9. Figure-family-specific defaults

| Figure family | Default dimensionality | Default text density | Default emphasis |
| --- | --- | --- | --- |
| microbial interaction | 2D | low-medium | organisms + transfer routes |
| integrated mechanism | 2D | medium | primary path + evidence hierarchy |
| material–microbe interface | light 2.5D | low-medium | contact/interface + electron direction |
| membrane/EET cutaway | 2D cutaway | medium | compartment + electron path |
| perturbation comparison | 2D | low-medium | matched contrast |
| graphical abstract | editorial 2D | low | single story path |
| environmental overview | editorial 2D / flat 2D | low | habitat + source/sink/gradient |

## 10. Anti-patterns

Reject or revise figures that show:

- photorealistic or glossy 3D cells/materials without scientific need;
- every process using the same arrow type;
- color used as the only evidence or process distinction;
- more than one competing focal pathway;
- dense text boxes replacing visual structure;
- arbitrary gradients or shadows;
- cells changing morphology between panels;
- unsupported mechanisms drawn with stronger visual weight than supported observations;
- material contact drawn as proven DIET/EET without an evidence distinction;
- a journal-specific “look” copied without understanding why the source layout works.

## 11. Consistency QA card

Before release, answer yes/no:

```text
[ ] Bath morphology and identity are consistent.
[ ] RP morphology and identity are consistent.
[ ] Recurrent metabolites/materials use stable visual tokens.
[ ] Main flow is readable without the legend.
[ ] Electron, carbon, metabolic, and causal relations are not conflated.
[ ] Supported and candidate links are distinguishable.
[ ] The layout matches the scientific relationship.
[ ] 2D/2.5D depth is restrained.
[ ] Text hierarchy is compact and readable.
[ ] The figure does not overstate evidence.
[ ] The image remains interpretable at target size.
```
