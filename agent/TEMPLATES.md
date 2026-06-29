# TEMPLATES.md

Read this file when creating or restructuring wiki pages.
Referenced by INGESTION.md (Steps 5–6) and REFINE_A.md (Steps A1–A3).

---

## 1. Page Templates

All pages use YAML frontmatter for structured metadata, followed by a markdown body.
The frontmatter `type` field is the only strictly required field; all others are strongly expected.

---

### 1.1 PHE_ — Phenomenon / Empirical Finding

```markdown
---
type: phenomenon
title: <full human-readable name>
confidence: established | debated | speculative
updated: YYYY-MM-DD
related:
  - REG_<slug>
  - PAR_<slug>
  - MOD_<slug>
tags: []
---

# <Phenomenon name>

## Description

<What is the phenomenon? Define it precisely, including conditions of observation.>

## Empirical Basis

<Synthesized summary across sources. Cite each claim: (@Key) primary, (@Key†) secondary.
Multiple sources for one claim: (@Key1, @Key2).>

## Key Parameters and Quantitative Signatures

<Specific numerical values: timescales, magnitudes, tuning widths, effect sizes.
Every number must be cited. Vague ranges without citations are not acceptable.>

## Generality

<Species, brain states, recording methods, behavioral conditions across which this holds.
Explicitly note where it breaks down or has not been tested.>

## Controversies

<Findings that contradict, qualify, or reframe the phenomenon.
All confidence changes explained here with citations.>

## Modeling Implications

<What must any model engaging with this phenomenon produce or respect?
Link to [[MOD_...]] pages.>
```

---

### 1.2 MOD_ — Model

```markdown
---
type: model
title: <full human-readable name>
subtype: mechanistic | normative | data-driven | behavioral
explanatory_role: how-possibly | how-actually | phenomenological
confidence: established | debated | speculative
updated: YYYY-MM-DD
related:
  - PHE_<slug>
  - REG_<slug>
  - PAR_<slug>
tags: []
---

# <Model name>

## Description

<What is this model? What problem was it designed to solve?
What idealization strategy does it use: Galilean (distortions intended for progressive de-idealization), minimalist (incompleteness is the point), or multiple-models (one of several incompatible models pursuing different representational ideals)?>

## Descriptive Target

<What regularities does this model fit? What data or phenomena is it empirically adequate to?
A phenomenon showing a different pattern falsifies the model with respect to its descriptive target.>

## Explanatory Scope

<At what level of organization does this model have genuine mechanistic or constitutive grounding?
If phenomenological at one level, state which — and state whether it is mechanistic at another level.
Level-relativity is mandatory: a model may be phenomenological at one level and mechanistic at another; both must be stated explicitly.>

## Formal Description

<Equations, variables, interpretations. $inline$ and $$block$$ LaTeX.
Always present equations before prose interpretation.>

## Core Assumptions

- **Assumption**: <statement>
  - *Biological justification*: <what supports it> (@Key)
  - *When violated*: <conditions under which this breaks down>

## Empirical Support

<Evidence that the model captures real phenomena. (@Key)>

## Empirical Challenges

<Evidence that contradicts, limits, or complicates the model. (@Key)>

## Comparison to Alternatives

<How does this differ from competing models? What does each handle better?>

## Controversies

<Ongoing disputes about validity, interpretation, or applicability.>

## Usage in the Literature

<Notable applications. What has this been used to explain or analyze? (@Key)>
```

---

### 1.3 THE_ — Neuroscientific Theory

```markdown
---
type: theory
title: <full human-readable name>
status: active-research-area | settled | abandoned
updated: YYYY-MM-DD
related:
  - PHE_<slug>
  - MOD_<slug>
  - REG_<slug>
tags: []
---

# <Theory name>

## Core Claims

<What does this theory assert? State the central theoretical commitments as precisely as possible. (@Key)>

## Explanatory Schema

<State the abstract pattern of explanation. Must satisfy three conditions:
1. Verbal and general: covers the full model family without fixing mathematical form.
2. Constraining: specify what would fail to instantiate it. A schema that excludes nothing is a slogan, not a schema.
3. Predictively inert alone: note which phenomena fall within scope but require specific model instances to test or falsify.
(@Key)>

## Model Family

<What formal models instantiate this theory? What do they share structurally?
Link to relevant [[MOD_...]] pages.>

## Mechanistic Grounding

<At what level of organization does this theory operate?
What mechanisms does it invoke, and which does it leave unspecified or treat as black boxes? (@Key)>

## Empirical Scope

<What phenomena is this theory designed to explain?
What is explicitly outside its scope or left for other frameworks?
Link to relevant [[PHE_...]] pages.>

## Controversies

<Disputed claims, competing interpretations, or unresolved debates within or about this theory.>

## Key Sources

<Foundational and landmark papers. (@Key)>
```

---

### 1.4 REG_ — Brain Region or Cell Type

```markdown
---
type: region
title: <full human-readable name>
confidence: established | debated | speculative
updated: YYYY-MM-DD
related:
  - PHE_<slug>
  - MOD_<slug>
  - PAR_<slug>
tags: []
---

# <Region or cell type name>

## Anatomical Identity

<Location, laminar structure, major subregions or subtypes. (@Key)>

## Physiology

<Firing rates, spiking patterns, intrinsic currents. All values cited. (@Key)>

## Connectivity

<Major inputs and outputs. Feedforward/feedback/lateral distinction.
Laminar, cell-type, and synaptic specificity where known. (@Key)>

## Functional Role(s)

<What computations or behaviors is this region/cell type implicated in? (@Key)>

## Controversies

<Disputed claims about anatomy, physiology, or function.>

## Modeling Considerations

<What properties must a model of this region capture?
What simplifications are common and when do they fail? Link to [[MOD_...]] pages.>
```

---

### 1.5 PAR_ — Experimental Paradigm or Dataset

```markdown
---
type: paradigm
title: <full human-readable name>
updated: YYYY-MM-DD
related:
  - PHE_<slug>
  - REG_<slug>
  - MOD_<slug>
tags: []
---

# <Paradigm or dataset name>

## Description

<What is this paradigm or dataset? What is the experimental logic or data structure?>

## What It Measures / Reveals

<What neural or behavioral variables does it give access to?
What phenomena has it been used to characterize? (@Key)>

## Standard Variants

<Common protocol variants and what they emphasize differently.>

## Limitations and Confounds

<Known confounds, what the paradigm cannot distinguish, species/state dependencies.>

## Key Studies and Datasets

<Landmark papers or publicly available datasets. (@Key) or (@Key†)>

## Relevance to This Project

<How is or could this paradigm be used in the current project's context?>
```

---

### 1.6 MET_ — Analysis Method or Algorithm

```markdown
---
type: method
title: <full human-readable name>
subtype: analysis | preprocessing | decoding | statistical
confidence: established | debated | speculative
updated: YYYY-MM-DD
related:
  - PHE_<slug>
  - MOD_<slug>
  - PAR_<slug>
tags: []
---

# <Method name>

## Description

<What does this method do? What input does it take and what output does it produce?>

## Key Assumptions

<What must be true of the data for the method to be valid?
What does it assume about the signal, noise, stationarity, or independence of observations?>

## Known Artifacts and Limitations

<What systematic biases or distortions does it introduce?
Under what conditions does it fail or produce misleading results? (@Key)>

## Standard Variants

<Common algorithmic or protocol variants and what they emphasize differently.>

## Software Implementations

<Key tools, packages, or reference implementations.>

## Usage in the Literature

<How has this been applied in neuroscience? What has it been used to measure or reveal? (@Key)>
```

---

## 2. wiki/index.md Structure

`wiki/index.md` is the agent's navigation entry point for the entire wiki. It must be kept current by every workflow that creates or modifies pages. The agent reads this file first when navigating the wiki, then follows links to relevant pages rather than scanning the full `pages/` directory.

```markdown
---
type: index
title: Wiki Root Index
updated: YYYY-MM-DD
---

# Wiki Index — <Project Name>

## Phenomena
| Page | Title | Confidence | Updated |
|------|-------|------------|---------|
| [PHE_place-cell-remapping](pages/PHE_place-cell-remapping.md) | Place cell remapping | established | 2025-03-10 |

## Models
| Page | Title | Confidence | Updated |
|------|-------|------------|---------|

## Methods & Analysis
| Page | Title | Confidence | Updated |
|------|-------|------------|---------|

## Theories
| Page | Title | Status | Updated |
|------|-------|--------|---------|

## Brain Regions & Cell Types
| Page | Title | Confidence | Updated |
|------|-------|------------|---------|

## Paradigms & Datasets
| Page | Title | Updated |
|------|-------|---------|
```

Links in `index.md` use relative markdown paths (`pages/TYPE_slug.md`), not `[[TYPE_slug]]` notation, so the file is navigable by both agents and standard markdown renderers.

Cross-links within page bodies continue to use `[[TYPE_slug]]` notation.

---

## 3. Conflict Resolution Rules

The agent is never permitted to silently choose one position over another when papers conflict.

### Conflict types

| Type | Description |
|------|-------------|
| Quantitative | Same measure, different values |
| Qualitative | Contradictory direction or existence of an effect |
| Interpretive | Same data, different conclusions |
| Scope | Both correct but under different conditions |

### Handling

**Quantitative and scope**: represent both values/conditions with citations. Note the likely source of discrepancy. Do not average or choose. Set confidence to `debated` if not already.

**Qualitative**: both positions in Empirical Basis with neutral framing. Structured Controversies entry:

```
### <Conflict title>
- **Position A**: <statement> (@Key1)
- **Position B**: <statement> (@Key2)
- **Possible resolution**: <if one exists>
- **Status**: unresolved | partially resolved | resolved
- **⚑ Human review requested**: <reason, if modeling-relevant>
```

**Interpretive**: represent both interpretations with citations. Do not adjudicate.

**Irreconcilable** (bearing on core modeling choices): add to Controversies, set confidence to `debated`, add to page header:

```
> ⚑ **Human review required**: Irreconcilable conflict between (@Key1) and (@Key2) on [topic].
> See Controversies section.
```

List all such flags in the session summary.

---

## 4. Citation Integrity Rules

**When writing or rewriting:**
- Every factual claim carries at least one citation
- Every quantitative value is cited — a number without a citation is never acceptable
- Confidence changes cite the motivating evidence in the Controversies section
- Method descriptions cite the original source of the method

**When reading existing pages:**
- Uncited factual claim, source identifiable: add the citation inline
- Uncited factual claim, source not identifiable: flag as `<!-- UNCITED: <claim summary>, flagged YYYY-MM-DD -->`
- Do not delete or rewrite a claim solely because it lacks a citation
- List all flags added in the session summary
