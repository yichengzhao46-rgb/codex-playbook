# Scientific Figure Style Router Matrix

## Purpose

This matrix converts a scientific communication task into a first-pass layout and visual-style decision. It is a routing aid, not a rigid template.

## Core routing matrix

| Scientific task | Primary purpose | Preferred layout | Preferred style family | Typical density | Reference-source language |
| --- | --- | --- | --- | --- | --- |
| Defined two-species metabolic exchange | microbial interaction | two-organism interaction | flat 2D mechanism | medium | ISME / Nature Microbiology / Nature Communications |
| Final model supported by several measurements | integrated mechanism | evidence-to-model or two-organism interaction | flat 2D mechanism | medium-high | ISME / Nature Communications |
| Soluble metabolite cross-feeding | microbial interaction + mechanistic pathway | two-organism interaction | flat 2D mechanism | medium | ISME / ES&T |
| Electron path across cell envelope | electron transfer | pathway/cutaway | 2D pathway/cutaway | medium | Nature Communications / EES |
| Cell–mineral or cell–semiconductor contact | material–microbe interface | zoom-in multiscale | soft 2.5D | medium | EES / Nature Communications |
| Conductive material connecting two organisms | material–microbe interface + electron transfer | central hub + two-organism interaction | soft 2.5D / flat hybrid | medium | EES / Nature Communications / Water Research |
| Oxygen/redox environmental stratification | environmental process | layered gradient | editorial 2D or flat 2D | low-medium | ISME / Nature Water / ES&T |
| One-factor condition comparison | comparative perturbation | mirrored comparison | flat 2D or editorial 2D | low-medium | Water Research / ES&T / Nature Communications |
| Treatment/control experimental setup | experimental design | linear flow or mirrored comparison | editorial 2D | low-medium | Water Research / ES&T |
| High-level research objective slide | conceptual overview | linear flow or central hub | editorial 2D | low | Nature / Science Advances-style storytelling language |
| Paper TOC / graphical abstract | graphical abstract | linear flow or central hub | editorial 2D | low | ES&T / Nature Communications |
| Habitat→microbe→interface mechanism | multiscale zoom | zoom-in multiscale | editorial 2D + soft 2.5D inset | medium | Nature Communications / Nature Water / EES |

## Bath–RP project routes

### Route A — methane-driven dark carbon fixation final mechanism

```text
Target: manuscript main figure
Purpose: integrated mechanism + microbial interaction
Message: methane oxidation by Bath provides transferable metabolic support associated with enhanced dark inorganic-carbon incorporation in the coculture
Density: medium-high
Layout: two-organism interaction, optionally evidence-to-model
Style: flat 2D mechanism
Reference language: ISME + Nature Communications
Core elements: CH4/O2, Bath, central diffusible-products lane, RP, energy/redox/CBB module
Evidence rule: distinguish community-level observations from species-resolved claims; keep individual candidate transfer routes bounded
```

### Route B — Bath–Se biohybrid hypothesis

```text
Target: proposal/future-work schematic or manuscript hypothesis figure
Purpose: material–microbe interface + electron transfer
Message: a self-assembled Bath–mineral/semiconductor interface may enable photoelectron-assisted microbial metabolism/carbon fixation
Density: medium
Layout: zoom-in multiscale
Style: soft 2.5D schematic
Reference language: EES + Nature Communications
Core elements: spherical Bath, Se/mineral surface or nanoparticles, light cue, e− path, methane metabolism, carbon-fixation readout
Evidence rule: label proposed photoelectron/EEU steps as candidate unless directly resolved
```

### Route C — 5% versus 25% O2 perturbation

```text
Target: mechanism-support comparison
Purpose: comparative perturbation
Message: oxygen availability alters the coculture phenotype and donor-output context
Density: medium
Layout: mirrored comparison
Style: flat 2D mechanism
Reference language: Water Research + ES&T + Nature Communications
Core elements: matched Bath/RP scenes, O2 condition label, methane oxidation, donor metabolites, carbon-fixation phenotype
Evidence rule: preserve identical geometry across conditions; do not imply high O2 directly causes every downstream transcriptional/metabolic change unless shown
```

### Route D — GAC-facilitated interspecies coupling / potential DIET

```text
Target: Objective 3 concept/mechanism schematic
Purpose: material–microbe interface + microbial interaction + electron transfer
Message: test whether a conductive interface can facilitate interspecies electron coupling beyond soluble transfer
Density: medium
Layout: Bath → GAC → RP with a parallel alternative-soluble-transfer lane
Style: soft 2.5D / flat hybrid
Reference language: EES + Nature Communications + Water Research
Core elements: Bath, porous GAC, RP, e− route, soluble H2/formate/acetate/mediator alternative
Evidence rule: conductive-material enhancement alone must not be rendered as proven DIET
```

### Route E — membrane-level Bath EET/EEU

```text
Target: mechanism or Objective 2 subfigure
Purpose: electron transfer
Message: resolve electron exchange across the Bath cell envelope and a selected extracellular interface
Density: medium-high
Layout: cell-envelope cutaway
Style: 2D pathway/cutaway
Reference language: Nature Communications + EES
Core elements: membrane layers, electron carriers/cytochromes only when supported, extracellular acceptor/donor, methane oxidation context
Evidence rule: distinguish known components, inferred route, and proposed reverse/uptake direction
```

### Route F — microoxic–anoxic environmental context

```text
Target: background/concept slide or ecological-context figure
Purpose: environmental process
Message: methane and oxygen overlap creates a dynamic interface where methanotroph activity and partner processes can coexist
Density: low
Layout: layered environmental gradient
Style: editorial 2D overview
Reference language: ISME + Nature Water
Core elements: habitat layer, CH4 upward flux, O2 downward flux, overlap zone, Bath/partner/mineral icons
Evidence rule: environmental analogy must not be drawn as if the exact defined coculture has been demonstrated in that field habitat
```

## Decision rules

### If the user says only “ISME style”

Do not stop at the journal label. Infer or ask internally:

- what scientific job the figure performs;
- whether the subject is interaction, pathway, environment, interface, experiment, or summary;
- how much information must be carried;
- whether 2.5D depth is functionally necessary.

Then use ISME as a reference-source filter rather than the route itself.

### If the figure contains a material

Do not automatically route to 2.5D. Use soft 2.5D only when porosity, surface contact, spatial interface, or conductivity needs a depth cue. Otherwise a flat material icon may be clearer.

### If the figure contains multiple evidence types

Do not create one arrow per assay. Use evidence-to-model structure or compact supporting annotations. Measurements support the model; they are not necessarily mechanistic steps.

### If the same science is needed for paper and PPT

Keep the scientific identities and evidence semantics stable, but re-route density and composition:

- paper: medium/high density, more mechanistic detail;
- PPT: low/medium density, larger objects and shorter labels;
- graphical abstract: low density, one dominant path.

### If several routes are hypothetical

Do not solve uncertainty by making every arrow dashed. Prioritize the main supported scaffold, then show only the few candidate branches needed to communicate the unresolved mechanism.

## Fast output format

For routine use, the router may return a compact decision card:

```text
Purpose:
Layout:
Style:
Density:
Reference language:
Key elements:
Arrow/evidence code:
Must not imply:
```

This is sufficient to drive image generation or a more detailed design brief.
