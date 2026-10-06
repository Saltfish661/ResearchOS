# Editable Figure Pipeline Design

Status: proposed subsystem design  
Target: ResearchOS V0.2 foundation, V0.3 image-to-editable bridge  
Snapshot date: 2026-10-06

## 1. Purpose

ResearchOS needs a figure pipeline that can produce publication-quality visuals without forcing the researcher to choose between:

- fully manual drawing,
- non-editable raster images,
- visually weak but technically editable diagrams,
- or AI-generated images that cannot be safely revised.

The Figure Pipeline therefore treats **editability, provenance, semantic structure, and scientific correctness** as first-class requirements.

Its central design rule is:

> Use structured rendering when the figure encodes scientific values; use image generation only as a visual-design aid when scientific geometry and values are not being inferred from the raster output.

## 2. Figure classes

ResearchOS classifies figures before choosing a renderer.

### 2.1 Data figures

Examples:
- line charts,
- bar charts,
- scatter plots,
- heatmaps,
- box/violin plots,
- ROC/PR curves,
- confusion matrices,
- ablation plots,
- performance/resource trade-off plots.

Preferred route:

`structured data -> figure spec -> deterministic renderer -> editable vector/output`

Do **not** use an image-generation model as the source of plotted scientific values.

Primary goals:
- numerical fidelity,
- reproducibility,
- traceability to experiment artifacts,
- editable labels/legends/axes,
- stable regeneration after data changes.

### 2.2 Scientific diagrams

Examples:
- method diagrams,
- system architecture,
- workflow diagrams,
- mechanism illustrations,
- data-flow diagrams,
- experimental setup schematics,
- conceptual overview figures.

Preferred route:

`scientific semantics -> figure spec -> editable rendering`

Optional route:

`scientific semantics -> image-model visual draft -> semantic reconstruction -> figure spec -> editable rendering`

The raster draft is never the authoritative scientific representation.

### 2.3 Illustrative / decorative visuals

Examples:
- cover art,
- poster background,
- decorative icons,
- non-quantitative conceptual imagery.

Image generation may be used directly when editability is not required.

If used inside a scientific figure, the generated element must be isolated as a decorative asset rather than merged with quantitative content.

## 3. Modules

### 3.1 figure-planner

Responsibilities:
- classify the figure,
- identify linked claims,
- define the figure's one-sentence message,
- choose visual grammar,
- define panels,
- define required labels, units, legends, annotations,
- determine editable-output requirements,
- select rendering route.

Inputs:
- claim IDs,
- experiment/source IDs,
- manuscript context,
- desired figure role,
- venue/output constraints,
- style preferences.

Outputs:
- `figure_spec.yaml`
- figure contract,
- required data/artifacts,
- recommended renderer/output targets.

### 3.2 figure-builder

Responsibilities:
- render the figure from a valid spec,
- preserve semantic groupings,
- export editable outputs,
- record data and rendering provenance,
- produce preview raster for inspection.

Supported MVP routes:

#### Data route
`CSV/JSON/table/experiment artifact -> chart renderer -> SVG/PDF/PPTX`

#### Diagram route
`figure_spec.yaml -> SVG/PPTX/draw.io-like structured output`

Future optional targets:
- Canvas/scene JSON,
- Figma-compatible scene representation,
- Mermaid for simple diagrams.

The builder must not invent missing values or labels.

### 3.3 figure-auditor

Responsibilities:
- validate scientific correctness,
- validate editability,
- validate visual consistency,
- validate provenance,
- compare manuscript text/caption to figure content.

Checks include:
- axis units,
- scales,
- legends,
- significant digits,
- panel labels,
- figure/table values vs source artifacts,
- readable final-size text,
- editable text objects,
- semantic grouping,
- vector/raster balance,
- raster resolution,
- unsupported claims implied by the visual,
- color accessibility,
- source traceability.

### 3.4 image-to-editable-bridge

Target: V0.3 unless an MVP proves sufficiently reliable earlier.

Purpose:
convert an image-assisted visual concept into a structured editable figure.

Preferred flow:

```text
scientific content
    ↓
semantic draft
    ↓
optional image model
    ↓
visual reference image
    ↓
layout / object / relation extraction
    ↓
semantic figure spec
    ↓
editable reconstruction
    ↓
SVG / PPTX / Canvas scene
```

The bridge performs **semantic reconstruction**, not blind bitmap vectorization.

## 4. Why bitmap tracing is insufficient

A raster-to-vector trace can produce technically valid SVG while remaining practically uneditable.

Typical failure modes:
- text converted into paths,
- arrows fragmented into arbitrary curves,
- boxes split into many unrelated paths,
- no logical grouping,
- gradients creating hundreds of nodes,
- hidden raster image embedded inside an SVG wrapper,
- no relationship between visual objects and scientific concepts.

ResearchOS therefore defines editability semantically.

## 5. Editability levels

Every figure receives an editability grade.

### E0 — Raster only
PNG/JPEG/WebP with no structured editable source.

### E1 — Vector shell
SVG/PDF exists, but text or components are flattened/path-heavy.

### E2 — Editable primitives
Text remains text; lines, arrows, shapes, chart marks are independently editable.

### E3 — Semantic groups
Objects are grouped by panel/module/series and maintain stable IDs.

### E4 — Regenerable semantic figure
The entire figure can be reproduced from `figure_spec.yaml` plus its source artifacts.

ResearchOS should target:
- data figures: **E4**
- scientific diagrams: **E3–E4**
- decorative visuals: E0–E2 may be acceptable.

## 6. Figure authority model

Scientific authority flows one way:

```text
source data / accepted claim / method definition
                ↓
            figure spec
                ↓
          renderer / image draft
                ↓
          visual figure output
```

A generated image cannot become evidence for a scientific claim.

If an image model invents:
- labels,
- values,
- mechanisms,
- modules,
- relationships,
- annotations,

those elements must be discarded unless separately supported by the scientific state.

## 7. Image-model-assisted design

Image models may be used for:
- composition exploration,
- layout inspiration,
- style exploration,
- icon concepts,
- visual hierarchy,
- decorative assets.

Examples of provider classes may include:
- GPT image-generation models,
- Google image-generation models,
- other user-configured providers.

ResearchOS should remain provider-agnostic.

### Required constraints

The prompt sent to an image model should distinguish:

- immutable scientific content,
- optional stylistic freedom,
- forbidden invented text/data,
- aspect ratio,
- panel count,
- intended visual hierarchy.

The visual output is marked:

`DRAFT_REFERENCE_ONLY`

until reconstructed into a semantic figure.

## 8. Semantic figure specification

`figure_spec.yaml` is the canonical description of a ResearchOS figure.

It stores:

- identity,
- figure class,
- scientific role,
- linked claims,
- source artifacts,
- panels,
- objects,
- relations,
- data mappings,
- style constraints,
- editability target,
- output targets,
- image-draft metadata when used.

A figure spec must separate:

### Scientific semantics
What the figure is asserting or displaying.

### Visual semantics
How those concepts are laid out.

### Rendering details
Fonts, spacing, line widths, palettes, export format.

This separation makes restyling possible without altering scientific content.

## 9. Figure manifest

`figure_manifest.yaml` records generated artifacts.

For each render:
- figure ID,
- spec version/hash,
- source artifacts,
- renderer,
- output files,
- editability grade,
- raster dependencies,
- preview,
- QA status,
- provenance,
- generation timestamp.

A manuscript should reference figure IDs, not unmanaged filenames.

## 10. Data-figure pipeline

### Input contract

A data figure must identify:
- experiment/source artifact,
- data table or result object,
- variable mappings,
- aggregation rule,
- uncertainty representation,
- ordering,
- filtering,
- units.

### Rendering

Preferred deterministic renderers:
- matplotlib,
- plotly,
- declarative SVG,
- other reproducible plotting systems.

### Output

MVP:
- SVG,
- PDF,
- PNG preview.

Preferred:
- editable PPTX for office-centric workflows.

Future:
- Canvas/scene JSON.

### Regeneration rule

Changing source data should require regeneration, not manual visual patching.

Manual edits to an E4 figure that change scientific data should invalidate its provenance status.

## 11. Diagram pipeline

Preferred semantic objects:

- module,
- process,
- dataset,
- actor,
- sensor,
- model,
- storage,
- decision,
- annotation,
- boundary,
- connector,
- group,
- panel.

Relations:
- flow,
- dependency,
- feedback,
- containment,
- temporal order,
- data transfer,
- causal hypothesis,
- comparison.

Each object receives a stable ID.

Example:

```text
NODE-HSI
NODE-LIDAR
NODE-FUSION

NODE-HSI --data_flow--> NODE-FUSION
NODE-LIDAR --data_flow--> NODE-FUSION
```

This allows later edits without visually reconstructing the whole figure.

## 12. PPTX strategy

PPTX is a first-class target because many researchers need to:
- edit labels quickly,
- reuse diagrams in presentations,
- satisfy "editable figure" requirements,
- hand figures to collaborators who do not use vector-design software.

PPTX export should prefer:
- native text boxes,
- native shapes,
- native connectors,
- grouped components,
- editable chart objects when feasible.

Avoid using a single full-slide raster image except for explicitly decorative content.

## 13. SVG strategy

SVG export should preserve:
- text as text,
- semantic IDs,
- groups,
- reusable markers for arrows,
- clean viewBox,
- no unnecessary bitmap embedding,
- minimal path complexity.

Audit should flag:
- huge path counts,
- all-text-as-path,
- embedded full-canvas raster,
- missing IDs/groups.

## 14. Canvas / scene representation

A future scene JSON may represent the figure as editable objects.

Suggested conceptual structure:

```yaml
scene:
  objects:
    - id: NODE-A
      type: rect
      x: 100
      y: 120
      width: 220
      height: 80
      text: Input data
  connectors:
    - from: NODE-A
      to: NODE-B
      type: arrow
```

The semantic spec remains authoritative; scene JSON is a render/edit representation.

## 15. Figure contract

Before rendering, every important figure should answer:

1. What single conclusion should the reader get?
2. Which claims does it support?
3. Which evidence/data does it display?
4. What does each panel do?
5. What visual encoding is scientifically meaningful?
6. What uncertainty must be shown?
7. What could a reviewer misread?
8. What editability level is required?

If these questions are unclear, the figure should not be generated yet.

## 16. Caption contract

Captions should include, where applicable:
- what is shown,
- key conditions,
- metric definition/units,
- aggregation,
- error-bar meaning,
- sample/run count,
- panel meaning,
- abbreviation definitions.

Do not put interpretation in the caption that exceeds the figure's evidence.

## 17. Figure QA

### Scientific QA
- values match source,
- units correct,
- aggregation documented,
- uncertainty correct,
- no unsupported interpolation,
- no misleading axis truncation without disclosure.

### Semantic QA
- labels match manuscript terms,
- module names stable,
- arrows represent actual relationships,
- panel ordering supports the narrative.

### Visual QA
- final-size readability,
- alignment,
- spacing,
- consistent typography,
- accessible contrast,
- legend clarity.

### Editability QA
- text editable,
- groups logical,
- arrows independent,
- plot series independently addressable when possible,
- no accidental flattening.

### Provenance QA
- source artifacts resolvable,
- spec version recorded,
- renderer/version recorded,
- generated output listed in manifest.

## 18. Human editing

Human modification is expected.

ResearchOS should support two editing modes:

### Cosmetic edit
Examples:
- move label,
- change font size,
- adjust spacing.

These do not invalidate scientific provenance if the content is unchanged.

### Scientific edit
Examples:
- change a plotted value,
- remove a data point,
- alter a label's scientific meaning,
- change an arrow relationship.

These require updating the figure spec/source and regenerating or recording an explicit provenance break.

## 19. Integration with ResearchOS

### Experiment Designer
Defines:
- metrics,
- uncertainty,
- comparison structure,
- expected figure roles.

### Result Auditor
Authorizes which result patterns and claim strength may be visualized.

### Paper Builder
Requests figures through figure contracts and links figure IDs to claims/sections.

### Paper Auditor
Checks manuscript-figure consistency and whether the visual overstates evidence.

### Submission Manager
Selects venue-compatible output bundles.

## 20. MVP

V0.2 MVP should implement:

### Figure Planner
- figure classification,
- claim/source linking,
- figure contract,
- basic panel plan.

### Figure Builder
Data:
- line,
- bar,
- scatter,
- heatmap.

Diagram:
- flowchart,
- architecture diagram.

Outputs:
- SVG,
- PDF,
- PNG preview,
- PPTX where practical.

### Figure Auditor
- source trace,
- labels,
- units,
- text editability,
- SVG group/path sanity,
- manuscript terminology consistency.

### Schemas
- `figure_spec.yaml`
- `figure_manifest.yaml`

## 21. V0.3 image-to-editable bridge

V0.3 may add:
- provider-agnostic image draft generation,
- layout/object extraction,
- semantic reconstruction,
- side-by-side draft vs editable render comparison,
- preservation of selected generated decorative assets,
- Canvas/scene output,
- optional Figma-like integration.

Success should be measured by:
- semantic fidelity,
- editability,
- reconstruction cleanliness,
- time saved versus manual redraw,

not pixel-level similarity to the generated raster draft.

## 22. Failure modes

Flag:
- using generated raster values as scientific evidence,
- claiming a traced SVG is "editable" when all text is paths,
- flattening a chart into a bitmap,
- image model inventing labels/mechanisms,
- manual scientific edits not reflected in provenance,
- visually attractive figure that no longer matches the method/results,
- excessive SVG path fragmentation,
- figure spec that mixes data truth with presentation choices,
- decorative AI imagery obscuring quantitative content,
- output format chosen solely for appearance rather than downstream editing needs.

## 23. Design decision

ResearchOS should treat figures as **versioned scientific artifacts**, not exported pictures.

The canonical hierarchy is:

```text
scientific evidence / method semantics
              ↓
        figure_spec.yaml
              ↓
     renderer / visual draft
              ↓
      editable render artifact
              ↓
      figure_manifest.yaml
              ↓
        manuscript / slides
```
