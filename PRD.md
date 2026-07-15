# PRD: Interactive Science-Communication Websites from Scientific Manuscripts

**A reusable Product Requirements Document and framework for turning a research
manuscript into an accessible, precise, visually coherent, interactive outreach website.**

| Field | Value |
| --- | --- |
| Framework version | 1.0.0 |
| Status of this document | Stable, reusable framework |
| License | Creative Commons Attribution 4.0 (CC BY 4.0). *(Default assumption; change to fit your policy)* |
| Provenance | Distilled from a first complete project: an interactive companion site for a peer-reviewed neuroimaging manuscript on how neurovascular coupling impairments reshape BOLD-based functional connectivity. That project is used throughout as the **worked example**. |
| DOI | [10.5281/zenodo.21356399](https://doi.org/10.5281/zenodo.21356399) (concept DOI, always the latest version) |
| How to cite | See [§10.4](#104-attribution-citation-and-licensing). |

> **Requirement language.** This document uses **MUST** (mandatory), **SHOULD**
> (strongly recommended; deviations must be justified), and **MAY** (optional) in
> the sense of RFC 2119. Items marked **(Default assumption)** are reasonable
> inferences, not confirmed requirements; override them freely.

> **How to read this as a template.** Anything in `{{DOUBLE_BRACES}}` is a
> manuscript-specific placeholder to be filled per project. Everything else is
> reusable across manuscripts. Section [§8](#8-manuscript-to-website-adaptation-workflow)
> and [CHECKLIST.md](CHECKLIST.md) tell you exactly what to swap.

---

## Table of contents

1. [Purpose and scope](#1-purpose-and-scope)
2. [Intended users and audiences](#2-intended-users-and-audiences)
3. [Scientific communication principles](#3-scientific-communication-principles)
4. [Explanation architecture](#4-explanation-architecture)
5. [Interactivity requirements](#5-interactivity-requirements)
6. [Visual and aesthetic system](#6-visual-and-aesthetic-system)
7. [Component design rules](#7-component-design-rules)
8. [Manuscript-to-website adaptation workflow](#8-manuscript-to-website-adaptation-workflow)
9. [Responsible communication for pre-review work](#9-responsible-communication-for-pre-review-work)
10. [Open-source and GitHub repository structure](#10-open-source-and-github-repository-structure)
11. [Content model and information architecture](#11-content-model-and-information-architecture)
12. [Accessibility, performance, and implementation constraints](#12-accessibility-performance-and-implementation-constraints)
13. [Output format and reuse](#13-output-format-and-reuse)
- [Appendix A: Semantic color token system (worked example)](#appendix-a-semantic-color-token-system-worked-example)
- [Appendix B: Component specification template](#appendix-b-component-specification-template)
- [Appendix C: Placeholder catalog](#appendix-c-placeholder-catalog)
- [Appendix D: Mathematical notation design checklist](#appendix-d-mathematical-notation-design-checklist)

---

## 1. Purpose and scope

### 1.1 Purpose
This framework exists to **transform a complex scientific manuscript into an
accessible, interactive, web-based explanation** without sacrificing scientific
accuracy. It is a planning and design contract: a scientist swaps in
manuscript-specific content and follows the reusable rules here to produce an
outreach website that is **precise, layered, visually coherent, and genuinely
interactive** rather than decorative.

### 1.2 What the framework helps you do
- Convert dense results, equations, and figures into a **graduated explanation**
  that a non-expert can enter and an expert can trust.
- Encode **scientific meaning into visual and interactive structure** (color,
  layout, annotation, interaction) so the design *is* part of the explanation.
- Communicate **uncertainty and status honestly**, especially for work that is
  not yet peer reviewed.
- Ship something **lightweight, durable, and cheap to host** (static-first), so
  the site outlives the news cycle of a paper.

### 1.3 Scope of applicability
The framework applies to outreach sites derived from:
- **Pre-review manuscripts** and **preprints** (arXiv, bioRxiv, medRxiv, etc.),
- **Peer-reviewed / published papers**,
- **Registered reports, datasets, methods papers, and other research outputs**.

It is **domain-agnostic**: the worked example is neuroimaging, but the rules
(notation design, layered explanation, honest caveats, interaction-for-understanding)
transfer to physics, biology, economics, ML, climate, and beyond.

### 1.4 Out of scope
- It is **not** a substitute for the manuscript, its data, or its code.
- It is **not** a quantitative reproduction environment. Interactive demos are
  explanatory instruments (see [§9](#9-responsible-communication-for-pre-review-work)).
- It does **not** mandate a specific frontend framework (see [§12.6](#126-technology-baseline-and-graceful-degradation)).

### 1.5 Reusability commitment
This PRD **MUST** be publishable in a public GitHub repository under an open
license so other scientists can fork, adapt, and reuse it. Repository structure,
attribution, and reuse rules are specified in [§10](#10-open-source-and-github-repository-structure).

---

## 2. Intended users and audiences

### 2.1 Primary users (who builds with this PRD)
| User | Needs the framework to provide |
| --- | --- |
| **Scientists / manuscript authors** | A path from paper to site that preserves accuracy and their voice. |
| **Research groups / labs** | A repeatable house style across multiple papers. |
| **Science communicators / press officers** | Guardrails against overstatement; ready explanatory scaffolds. |
| **Designers** | A concrete visual and component system to implement. |
| **Developers** | Actionable, testable requirements and accessibility budgets. |

### 2.2 Target audiences (who reads the resulting website)
Non-experts and the scientifically curious public; **students**; **researchers
from adjacent fields**; **journalists**; **funders**; **collaborators and
reviewers**; and **peers in the same field** who want the rigorous layer.

### 2.3 Serving multiple expertise levels without diluting accuracy
The site **MUST** support at least three reader depths **simultaneously**, using
**progressive disclosure** rather than dumbed-down prose:
- **Layer 1 (Intuition):** plain-language motivation, metaphor, and a picture,
  before any formalism.
- **Layer 2 (Mechanism):** the conceptual model, key variables, and how they
  interact, with light math.
- **Layer 3 (Formalism):** equations, assumptions, parameters, limitations, and
  the manuscript's exact results.

**Rule:** simplifications live in Layer 1–2 prose; the *full* precision is always
reachable in Layer 3 and never contradicted by the simpler layers. When a simpler
layer is an approximation, it **MUST** say so and link down to the precise version.

---

## 3. Scientific communication principles

### 3.1 Accuracy and proximity to the manuscript
- Every scientific claim on the site **MUST** be traceable to the manuscript (or
  an explicitly cited external source). No claim should exceed what the paper supports.
- The site **SHOULD** distinguish, visibly and verbally, between:
  **intuition** (a mental model), **interpretation** (what results might mean),
  **formal results** (what was actually measured/derived), **open questions**,
  and **limitations**. Never let a metaphor read as a result.
- **Worked-example rule (from the project):** where a metaphor is physically
  incomplete, keep it *and* add a one-line correction. E.g. an MRI scanner
  "senses how much deoxyhemoglobin is present via magnetic field effects; it
  reads magnetism, not literal color; the red/blue picture is a visual shorthand."

### 3.2 Presenting equations, notation, definitions, assumptions, limitations, terminology
- **Mathematical notation MUST be *designed*, not dumped.** Follow the five
  pillars of Fred Hohman's *Awesome Mathematical Notation Design* (Color,
  Layout, Annotations, Gestalt, Interactivity), credited alongside Piotr Migdał's
  *Equations Explained Colorfully*, BetterExplained, and Stuart Riffle. See
  [Appendix D](#appendix-d-mathematical-notation-design-checklist).
- **One consistent, meaningful color per concept**, reused in equations, figures,
  sliders, and prose, so the symbols and graphics read as one picture. Pair color
  with **bold weight** (redundant encoding) so it survives color-vision deficiency.
- **Annotate** each sub-expression in plain language directly beneath it
  (`\underbrace{…}_{\text{…}}`). **De-emphasize** calibration constants and
  scaffolding (mute to gray) so the meaningful variables carry the eye.
- **Equations MUST have an accessible fallback**: rendered math (KaTeX/MathJax
  with MathML) *and* an unambiguous text form (e.g. `v^(1/alpha)`, never a
  superscript that flattens to `v1/alpha` when copied or read aloud).
- **Definitions:** every specialized term gets a tooltip or glossary entry on
  first use; a full **glossary** and a **symbol table** are required (see [§7](#7-component-design-rules)).
- **Assumptions and limitations are first-class content**, not footnotes: state
  the model's assumptions, the parameter values, and what the result does *not* show.

### 3.3 When to simplify, preserve formalism, or layer
- **Simplify** in the entry layer (motivation, metaphor, one-sentence takeaways).
- **Preserve formalism** whenever the exact form carries meaning a paraphrase would
  lose (units, exponents, scaling, error terms). Do not "round off" the math.
- **Layer** whenever both are needed: show intuition first, put the rigorous
  version one click away (`<details>` / "Show me the math"), and keep them consistent.

### 3.4 Separating model layers (a reusable pattern)
When a site shows a *simplified demo* alongside the *manuscript's real model*, it
**MUST** separate the layers explicitly. The worked example uses a labeled cascade:
1. **Underlying physics** (what actually produces the signal),
2. **Domain model as used in the field** (the standard/classic model),
3. **The manuscript's specific model** (what this paper changed),
4. **The demo's simplified engine** (what the sliders actually compute).
Each layer is headed, ordered, and cross-referenced, so no reader mistakes the
toy for the paper. Pair this with a **paper-vs-demo comparison table** ([§7](#7-component-design-rules)).

### 3.5 Communicating pre-review / preprint work responsibly
See [§9](#9-responsible-communication-for-pre-review-work) for the full rules.
Minimum: label manuscript status prominently, hedge preliminary claims, avoid
causal/clinical overreach, and link to the manuscript, data, and code.

---

## 4. Explanation architecture

### 4.1 The ramp (reusable entry structure)
The site **MUST** implement a gradual on-ramp so a non-expert is never dropped
into formalism. Canonical order:

```
Motivation ─▶ Intuition / metaphor ─▶ Core question ─▶ Conceptual mechanism
    ─▶ Interactive exploration ─▶ Figures & results ─▶ Mathematical detail
    ─▶ Manuscript-level interpretation ─▶ Limitations ─▶ Citations & reproducibility
```

**Worked example:** the project opens with a "Meet the {{CENTRAL_METAPHOR}}"
primer, *the picture before the equations*, using an animated, narrated single
concept before any demo or math. Reuse this "primer-first" move.

### 4.2 Progression from intuition to formalism
- Start each major concept with a **one-paragraph plain-language motivation** and a
  **single concrete image or animation**.
- Introduce variables **one at a time**, each color-coded to the concept it will
  keep for the rest of the site.
- Reveal the governing equations only after the reader has seen the behavior they
  describe (ideally by manipulating it interactively first).
- End each concept with a **takeaway callout** stating the transferable insight.

### 4.3 Reusable explanation layers
| Layer | Reader | Content pattern | UI vehicle |
| --- | --- | --- | --- |
| **Beginner** | Curious public, students | Metaphor, animation, "what and why" | Primer section, concept cards, narrated animation |
| **Intermediate** | Adjacent-field researchers | Mechanism, variables, qualitative model | Interactive demos, annotated figures, tooltips |
| **Expert** | In-field peers, reviewers | Equations, parameters, assumptions, exact results | "Show me the math" `<details>`, symbol table, methods, limitations |

### 4.4 Moving between conceptual and technical detail
- Every technical section **MUST** be reachable from, and return to, a conceptual
  summary (in-page anchors + a persistent nav).
- Rigorous detail **SHOULD** default to collapsed (`<details>`), so the page reads
  smoothly for beginners but expands fully for experts.
- Conceptual claims that have a formal counterpart **SHOULD** link directly to it
  ("see the equation" / "see the methods").

---

## 5. Interactivity requirements

### 5.1 Principle: interactivity serves understanding
Every interactive element **MUST** teach something that static media cannot. If an
interaction does not change what the reader understands, it is decoration and
**SHOULD** be removed. Interactions **SHOULD** let the reader *test a hypothesis*
("what happens to the result if I change X?").

### 5.2 Reusable interaction patterns (extracted from the project)
| Pattern | What it does | Scientific job |
| --- | --- | --- |
| **Concept sliders** | Drive a model parameter; thumb color-matched to the concept's curve | Make cause→effect legible in real time |
| **Draggable curves / fit lines** | Drag a data or fit line to nudge the underlying parameters | Reverse the intuition: outcome→parameter |
| **Live derived metrics** | Recompute a summary statistic (e.g. a correlation) on every change | Connect manipulation to the paper's headline metric |
| **Parameter-sweep heatmap** | 2-D field of an outcome over two parameters | Show the whole landscape, not one point |
| **Hover readouts / crosshair pinning** | Sample values at a point; pin a synced crosshair across linked plots | Support precise inspection |
| **Narrated play/reset animation** | Step an animation with text narration and a reset | Tell a causal story with a controllable timeline |
| **Progressive-disclosure panels** | `<details>` "Show me the math", "Show assumptions" | Layer expert detail without cluttering |
| **Per-term equation tooltips** | Hover a symbol for a plain-language definition | Make notation self-documenting |
| **Concept cards & annotations** | Chunk ideas; label figure parts | Gestalt grouping of related ideas |

### 5.3 Interactivity must be scientifically valid
- Interactive outputs **MUST** be consistent with the manuscript's direction of
  effect, even when simplified. A demo may be qualitative but **MUST NOT** invert
  or misrepresent the science.
- Where a demo simplifies, the simplification **MUST** be disclosed at or near the
  control (a hint line, a "toy approximation" label, or a "Show assumptions" panel).
- Numerical values produced by demos **MUST** be framed as model- and
  noise-dependent, **not** quantitative predictions, unless they truly reproduce
  the paper.

### 5.4 Accessibility & usability per interactive element
Each control **MUST**:
- Be operable by **keyboard** (native `<input type="range">`, buttons, and
  `<details>` are preferred for this reason).
- Expose an accessible **name and current value** (visible label + `aria` where needed).
- Provide a **non-hover path** to any information shown on hover (tooltips must also
  appear on focus/tap, or the same content must exist in the glossary/table).
- Respect **`prefers-reduced-motion`** (see [§12](#12-accessibility-performance-and-implementation-constraints)).
- Degrade gracefully: if scripting fails, the underlying figure, caption, and
  math fallback still convey the point.

### 5.5 Reproducible, inspectable, manuscript-linked
- The **model and parameters** behind each demo **MUST** be stated on the page
  (inline hint, "Show assumptions", or the methods/glossary).
- Demos **SHOULD** be deterministic where possible (seeded randomness) so a reader
  sees the same thing you describe.
- Each demo **SHOULD** name the manuscript concept it illustrates and link to the
  relevant figure/section.

---

## 6. Visual and aesthetic system

### 6.1 Visual identity (extracted from the project)
Elegant, lightweight, **academic but not sterile**: generous whitespace, a light
background, one clean sans-serif for text, restrained accent colors that all carry
scientific meaning, and inline SVG for figures. The design should feel like a
well-typeset paper that happens to be interactive.

### 6.2 Layout & spacing
- Centered content column with comfortable max width (**~1100–1200 px**,
  *(Default assumption)*) and section-level vertical rhythm.
- Clear **section eyebrow → title → intro → content** pattern for every major section.
- Demos use a consistent **two-panel** layout (controls/inputs beside outputs).

### 6.3 Typography
- One primary sans-serif for UI/body (worked example: **Inter**), a math font via
  KaTeX for equations. *(Default assumption: system-font fallback stack.)*
- Establish a type scale for eyebrow, title, body, hint/caption; keep body ≥ 16 px.
- Use **weight** (not just size/color) for emphasis, to reinforce redundant encoding.

### 6.4 Color as scientific encoding (core rule)
- Maintain a **semantic color token table**: one hue per concept, defined once and
  reused in equations, curves, sliders, legends, and prose. See [Appendix A](#appendix-a-semantic-color-token-system-worked-example).
- **Bridge equation colors to figure colors**: a symbol and its curve share the hue.
- Reserve **muted gray** for calibration constants and scaffolding so the eye lands
  on the meaningful variables.
- Ensure text/background contrast meets **WCAG AA** (see [§12](#12-accessibility-performance-and-implementation-constraints)).

### 6.5 Cards, panels, callouts (house rule)
- **No accent side bars.** Cards, callouts, and notes **MUST NOT** use a colored
  `border-left`/edge stripe. Use a **plain, homogeneous, very light background**
  (worked example: `#f8fafc`) with no border or a single uniform subtle one. Keep
  emphasis in the content, not a decorative edge.
- Panels group one idea; captions and hints sit in muted small text beneath.

### 6.6 Tooltip definitions & hover states (reusable spec)
The project's tooltip aesthetic (reuse it for consistency):
- Dark, softly-blurred card with a subtle gradient background; **1–1.5 px border
  tinted to the concept's color**; concept-colored bold title + lighter description.
- Appears on **hover *and* focus/tap**; positioned near the cursor and flipped to
  stay on-screen; `cursor: help` on hoverable symbols.
- The **same content** is duplicated in the glossary/symbol table so it is never
  hover-only (accessibility).

### 6.7 Diagrams, notation, captions
- Figures **SHOULD** be inline **SVG** rendered by the site's own code (crisp,
  themeable, animatable) rather than raster images, except for photographs/logos.
- Every figure has a **caption** and, where relevant, **on-figure annotations**
  color-matched to the concepts.
- Equations rendered with **KaTeX/MathJax**, color-coded and annotated per [§3.2](#32-presenting-equations-notation-definitions-assumptions-limitations-terminology).

### 6.8 Animation & transitions
- Motion is **purposeful and calm**: fade-in on scroll (IntersectionObserver),
  smooth state transitions, narrated stepwise animations for causal stories.
- All non-essential motion **MUST** be disabled under `prefers-reduced-motion`.
- Avoid autoplaying loops that distract from reading.

### 6.9 Elegance & restraint
Prefer fewer colors used meaningfully over many used decoratively. Whitespace is a
feature. The site should stay **fast and light** ([§12](#12-accessibility-performance-and-implementation-constraints)).

### 6.10 Typographic house style *(Default assumption; adopt or drop)*
- **No em dashes** in body copy; use commas, parentheses, colons, or a middot
  separator. (Carried from the worked example's style guide.)
- En dashes are fine for numeric ranges (e.g. `0.01–0.1 Hz`).

---

## 7. Component design rules

Each component below is specified as: **Purpose · Content · Visual · Interaction ·
Accessibility · Placeholders**. Use the template in [Appendix B](#appendix-b-component-specification-template)
to add project-specific components.

### 7.1 Landing / hero
- **Purpose:** orient in 10 seconds: what, who, status, where to read more.
- **Content:** title, one-line plain-language subtitle, authors, **manuscript
  status badge**, primary actions (Read the paper · Try the demo · Cite).
- **Visual:** centered, generous whitespace, optional single hero graphic/logo.
- **Interaction:** anchor links to sections; buttons to external manuscript/data.
- **Accessibility:** `<h1>` is the title; buttons are real links/buttons.
- **Placeholders:** `{{TITLE}}`, `{{ONE_LINE_SUMMARY}}`, `{{AUTHORS}}`, `{{STATUS}}`, `{{PAPER_URL}}`, `{{CITATION}}`.

### 7.2 Manuscript-summary card
- **Purpose:** the paper in one card: question, approach, headline finding.
- **Content:** central question, method in a phrase, key result, and the "so what".
- **Visual:** homogeneous light card (no side bar), muted metadata line.
- **Placeholders:** `{{RESEARCH_QUESTION}}`, `{{METHOD}}`, `{{KEY_FINDING}}`, `{{IMPLICATION}}`.

### 7.3 Concept card
- **Purpose:** one idea, chunked (Gestalt common-region).
- **Content:** short heading with the concept's **color**, 2–4 sentence explanation.
- **Interaction:** none required; may reveal detail on click.
- **Placeholders:** `{{CONCEPT_NAME}}`, `{{CONCEPT_COLOR}}`, `{{CONCEPT_BLURB}}`.

### 7.4 Equation block
- **Purpose:** present formalism legibly and accessibly.
- **Content:** KaTeX equation with color-coded, bold, annotated terms; a plain-text
  fallback with explicit exponents; optional per-term tooltips.
- **Visual:** centered, light card, horizontally scrollable on overflow.
- **Interaction:** hover/focus a symbol → definition tooltip.
- **Accessibility:** MathML output; `aria-label` or unambiguous fallback text.
- **Placeholders:** `{{TEX}}`, `{{TERM_DEFINITIONS}}`, `{{FALLBACK_TEXT}}`.

### 7.5 Figure card (interactive or static)
- **Purpose:** show a result or mechanism.
- **Content:** inline SVG figure, caption, on-figure annotations, optional controls.
- **Interaction:** sliders/hover/pin per [§5](#5-interactivity-requirements); or none if static.
- **Accessibility:** `role="img"` + `aria-label` (static) or labeled controls (interactive).
- **Placeholders:** `{{FIGURE_SVG_OR_DEMO}}`, `{{CAPTION}}`, `{{CONTROLS}}`.

### 7.6 Tooltip definition
- **Purpose:** define a term/symbol in context.
- **Content:** concept-colored title + one-sentence description.
- **Interaction/Accessibility:** hover **and** focus/tap; mirrored in glossary.
- **Placeholders:** `{{TERM}}`, `{{DEFINITION}}`, `{{CONCEPT_COLOR}}`.

### 7.7 Glossary entry & 7.8 Symbol table
- **Purpose:** a complete, scannable reference of terms and symbols.
- **Content:** term/symbol · meaning · (symbol table also: units/normalization).
- **Visual:** simple table/grid; symbol column in the math font.
- **Placeholders:** `{{TERMS[]}}`, `{{SYMBOLS[]}}`.

### 7.9 Expandable technical note ("Show me the math" / "Show assumptions")
- **Purpose:** layer expert detail without cluttering the beginner path.
- **Content:** derivations, model layers, parameters, assumptions.
- **Interaction:** native `<details>`/`<summary>`, collapsed by default.
- **Placeholders:** `{{TECHNICAL_DETAIL}}`.

### 7.10 Comparison panel ("paper vs. demo" / model-vs-model)
- **Purpose:** prevent overinterpretation by contrasting the manuscript with the demo.
- **Content:** rows for signal/model, inputs, noise, sampling, purpose, valid use.
- **Visual:** compact table, muted, permanent (not hidden).
- **Placeholders:** `{{COMPARISON_ROWS}}`.

### 7.11 Limitation note
- **Purpose:** state honestly what the result does not show.
- **Content:** concise, specific caveats tied to assumptions.
- **Visual:** homogeneous light callout (no side bar).
- **Placeholders:** `{{LIMITATIONS}}`.

### 7.12 Citation block
- **Purpose:** make the work citable and findable.
- **Content:** full reference, DOI, BibTeX, manuscript status.
- **Placeholders:** `{{CITATION}}`, `{{DOI}}`, `{{BIBTEX}}`.

### 7.13 Reproducibility / GitHub links
- **Purpose:** connect to data, code, and version history.
- **Content:** links to repo, data archive (e.g. Zenodo/OSF), supplementary materials.
- **Placeholders:** `{{CODE_URL}}`, `{{DATA_URL}}`, `{{SUPP_URL}}`.

### 7.14 Social preview / share card
- **Purpose:** control how the site looks when its link is shared (social media,
  chat, messaging, search). The share card is often the *first* thing a potential
  reader sees, before they visit; a missing or generic card suppresses reach.
- **Content:** a single **1200x630** image (the Open Graph standard; GitHub's
  repo social preview uses **1280x640**) carrying the title, a one-line summary,
  and the site's visual identity. Plus `<meta>` tags in `<head>`: `og:title`,
  `og:description`, `og:image` (an **absolute** URL), `og:type`, `og:url`,
  `twitter:card` (`summary_large_image`), and `twitter:image`. Also set
  `og:image:secure_url` (the same absolute HTTPS URL) and `og:image:type`
  (e.g. `image/png`): WhatsApp and other Facebook-crawler clients favour these
  and are more likely to render the image reliably.
- **Visual:** reuse the site's own design language, so the card and the page read
  as one system: the semantic colour palette ([§6.4](#64-color-as-scientific-encoding-core-rule)),
  the title type, and a small motif (e.g. a colour-coded equation or key figure).
  Keep text large and high-contrast; assume it is viewed as a thumbnail. Author it
  as an **SVG** and rasterise to PNG, so edits (title, DOI, version) are a re-render,
  not a redraw.
- **Interaction behavior:** none. It is metadata plus a static image.
- **Accessibility requirements:** the image is decorative *metadata*, but provide a
  meaningful `og:image:alt`. Never put information in the card that exists *only*
  there: it must restate content already on the page.
- **Manuscript placeholders:** `{{OG_IMAGE_URL}}` (absolute), `{{SITE_URL}}`,
  `{{TITLE}}`, `{{ONE_LINE_SUMMARY}}`.
- **Note:** GitHub repository social previews are **not** set from the repo files;
  upload the image under *Settings > Social preview*. Social platforms cache
  cards aggressively: use their card debuggers to force a re-scrape after changes.

---

## 8. Manuscript-to-website adaptation workflow

### 8.1 Repeatable workflow
1. **Extract the spine:** central research question, motivation, and the single
   headline finding. Write each in one plain sentence.
2. **Inventory the science:** methods, mathematical structures, datasets, key
   figures, parameters, assumptions, limitations, and broader implications.
3. **Pick the central metaphor / entry image** for the beginner layer.
4. **Build the semantic color table** ([Appendix A](#appendix-a-semantic-color-token-system-worked-example)):
   one hue per core concept; reuse everywhere.
5. **Design the notation** ([Appendix D](#appendix-d-mathematical-notation-design-checklist))
   for each equation you will show.
6. **Choose interactions** ([§5](#5-interactivity-requirements)) that let readers
   test the paper's key relationships; define each demo's model, parameters, noise, and caveats.
7. **Draft the content model** ([§11](#11-content-model-and-information-architecture))
   and fill placeholders.
8. **Apply responsible-communication rules** ([§9](#9-responsible-communication-for-pre-review-work)):
   status badge, hedging, links.
9. **Meet accessibility/performance budgets** ([§12](#12-accessibility-performance-and-implementation-constraints)).
10. **Review** against [CHECKLIST.md](CHECKLIST.md) with a domain expert *and* a non-expert.

### 8.2 Reusable vs. manuscript-specific
| Reusable across projects | Manuscript-specific (swap per paper) |
| --- | --- |
| Explanation ramp & layers ([§4](#4-explanation-architecture)) | Central question, findings, metaphor |
| Interaction patterns ([§5](#5-interactivity-requirements)) | The specific model, parameters, demos |
| Visual/aesthetic system ([§6](#6-visual-and-aesthetic-system)) | The concept→color assignments |
| Component rules ([§7](#7-component-design-rules)) | Equations, figures, glossary, symbol table |
| Responsible-communication rules ([§9](#9-responsible-communication-for-pre-review-work)) | Status, caveats, links |
| Repo structure ([§10](#10-open-source-and-github-repository-structure)) | Citation, data/code URLs |
| Accessibility/performance budgets ([§12](#12-accessibility-performance-and-implementation-constraints)) | Content that must stay readable on mobile |

### 8.3 Checklist
The authoritative, runnable checklist lives in **[CHECKLIST.md](CHECKLIST.md)**.

---

## 9. Responsible communication for pre-review work

### 9.1 Label manuscript status prominently
A **status badge MUST** appear in the hero and near the citation, using one of:
`Preprint` · `Under review` · `Accepted` · `Published` · `Working paper`.
Include the venue/DOI when available and the date/version.

### 9.2 Communicate uncertainty and non-final status
- For non-peer-reviewed work, add a visible line: *"This describes a
  {{STATUS}} manuscript; findings are preliminary and may change after review."*
- Prefer **hedged verbs** ("suggests", "is consistent with") over
  causal/definitive ones for interpretation-level claims.

### 9.3 Do not overstate
- **MUST NOT** assert causal or clinical/real-world implications beyond what the
  manuscript supports.
- Numbers from simplified demos **MUST** be labeled model/noise-dependent, not
  predictions.
- Distinguish **what was shown** from **what it might mean** ([§3.1](#31-accuracy-and-proximity-to-the-manuscript)).

### 9.4 Link generously
Provide links to the **manuscript, data, code, supplementary materials, and
version history** wherever they exist (preprint server, journal DOI, Zenodo/OSF,
GitHub/GitLab). Reproducibility links are a requirement, not a nicety.

### 9.5 Pedagogical-tool disclaimer (reusable)
If the site includes simplified demos, include a prominent disclaimer stating they
are **educational tools, not the peer-reviewed analysis**, and **not for reanalysis,
clinical inference, or benchmarking**, plus the paper-vs-demo table ([§7.10](#710-comparison-panel-paper-vs-demo--model-vs-model)).

---

## 10. Open-source and GitHub repository structure

### 10.1 Recommended layout (of the framework repo)
```
science-communication-prd/
├── README.md                     # What this is, quick start, how to adapt
├── PRD.md                        # This document (the framework)
├── CHECKLIST.md                  # Manuscript-adaptation checklist
├── CONTRIBUTING.md               # How others improve the framework
├── LICENSE                       # CC BY 4.0 for docs (default assumption)
├── CITATION.cff                  # Machine-readable citation for the framework
├── templates/
│   ├── component-spec.md         # Blank component spec (Appendix B)
│   ├── color-tokens.md           # Blank semantic color table (Appendix A)
│   └── content-model.md          # Blank section-by-section content plan (§11)
├── examples/
│   └── neurovascular-modeling/   # The worked example: notes + links + screenshots
└── assets/                       # Shared diagrams/screenshots for the docs
```
*(A project built **from** this framework is a separate repo; it MAY copy
`CHECKLIST.md` and the `templates/` into its own `docs/`.)*

### 10.2 Recommended files for a *derived project* repo *(Default assumption)*
`index.html` (or app), `README.md` (with status badge + links), `LICENSE` (code +
content), `CITATION.cff`, `data/` or links, and a short `docs/adaptation-notes.md`
recording the concept→color map and demo assumptions.

### 10.3 Responsible reuse
Forks **MUST** preserve the scientific-integrity and accessibility requirements
([§3](#3-scientific-communication-principles), [§9](#9-responsible-communication-for-pre-review-work),
[§12](#12-accessibility-performance-and-implementation-constraints)); these are
the point of the framework, not optional. Adapters **SHOULD** keep the layered
explanation and honest-caveat patterns even when restyling.

### 10.4 Attribution, citation, and licensing
- **License:** documentation under **CC BY 4.0**; code samples under **MIT**.
  Set explicitly in `LICENSE`.
- **Attribution:** retain credit to this framework and to the notation-design
  lineage (Hohman; Migdał; BetterExplained; Riffle) where the notation rules are used.

**Citing this framework.** Cite the **concept DOI**, which always resolves to the
latest version:

> Archila-Meléndez, M. E. (2026). *Interactive Science-Communication Website
> Framework (PRD)* (v1.0.0). Zenodo. https://doi.org/10.5281/zenodo.21356399

| DOI | Resolves to |
| --- | --- |
| `10.5281/zenodo.21356399` | All versions (cite this one) |
| `10.5281/zenodo.21356400` | Version `v1.0.0` specifically |

**Citing your own derived site.** Provide a `CITATION.cff` in your project and
archive a release (e.g. via Zenodo) so the site itself is citable. Suggested form:

> *"{{YOUR_NAME}} et al. {{SITE_TITLE}}. {{YEAR}}. {{REPO_URL}}. {{DOI}}.
> Built with the Interactive Science-Communication Website Framework,
> https://doi.org/10.5281/zenodo.21356399."*

---

## 11. Content model and information architecture

### 11.1 Reusable section map
| # | Section | Role | Reader level | Manuscript placeholder |
| --- | --- | --- | --- | --- |
| 1 | **Landing / hero** | Orient, status, actions | All | `{{TITLE}}`, `{{STATUS}}`, `{{PAPER_URL}}` |
| 2 | **Scientific motivation** | Why this matters | Beginner | `{{MOTIVATION}}` |
| 3 | **Conceptual background** | Mental model + metaphor | Beginner→Intermediate | `{{METAPHOR}}`, `{{CONCEPTS}}` |
| 4 | **Core result** | The headline finding | All | `{{KEY_FINDING}}` |
| 5 | **Interactive exploration** | Test the relationships | Intermediate | `{{DEMOS}}` |
| 6 | **Mathematical details** | Formalism, layered | Expert | `{{EQUATIONS}}`, `{{SYMBOLS}}` |
| 7 | **Manuscript connection** | Map demo↔paper; methods | Intermediate→Expert | `{{METHODS}}`, `{{COMPARISON}}` |
| 8 | **Limitations** | What it does not show | All | `{{LIMITATIONS}}` |
| 9 | **Glossary & symbols** | Reference | All | `{{TERMS}}`, `{{SYMBOLS}}` |
| 10 | **Citations & reproducibility** | Cite, data, code | All | `{{CITATION}}`, `{{CODE_URL}}`, `{{DATA_URL}}` |
| 11 | **Further reading** | Context & next steps | All | `{{FURTHER_READING}}` |

### 11.2 Movement between levels
- A **persistent navigation** exposes the section map; anchors allow jumping in
  and out of technical detail.
- Technical sections default to collapsed detail; conceptual summaries always
  precede them and link down.
- The **glossary, symbol table, and comparison panel** are reachable from anywhere.

---

## 12. Accessibility, performance, and implementation constraints

> Accessibility and performance are **core science-communication requirements**,
> not optional polish: an explanation that a reader cannot perceive, operate, or
> load has failed to communicate.

### 12.1 Keyboard & focus
All interactive controls **MUST** be keyboard-operable with visible focus. Prefer
native elements (`<input type="range">`, `<button>`, `<a>`, `<details>`).

### 12.2 Contrast & readable type
Text/background and essential graphical contrast **MUST** meet **WCAG 2.1 AA**.
Body text ≥ 16 px; do not encode meaning by color alone (pair with weight/shape/label).

### 12.3 Screen readers & semantics
Use **semantic HTML** (landmarks, headings in order, `<table>` for tabular data,
`<figure>`/`<figcaption>`). Equations render **MathML**; figures have `aria-label`;
hover-only content is mirrored in text (glossary/table).

### 12.4 Reduced motion
Honor **`prefers-reduced-motion`**: disable scroll/animation effects and
autoplaying motion; provide static equivalents.

### 12.5 Mobile & responsive readability
Layout **MUST** reflow to a single column on small screens; equations scroll
horizontally rather than overflow; sliders/plots remain usable by touch; captions
and math stay legible. Test at ~360 px width.

### 12.6 Technology baseline and graceful degradation
*(Default assumption: the whole of §12.6.)*

- **Static-first**: a single-file or few-file static site (HTML + CSS + vanilla
  JS + KaTeX) hosted on GitHub Pages is the recommended lightweight baseline; a
  framework (React/Svelte/etc.) is permitted if the accessibility and performance
  budgets are met.
- **No mandatory build step** for the baseline; edits are immediately previewable.
- **Graceful degradation:** if JS fails, figures/captions/math fallbacks and all
  prose still convey the science. Load fast (defer non-critical scripts; inline
  SVG; avoid heavy media).

### 12.7 Performance budget *(Default assumption)*
Target a near-instant first paint on a mid-range phone: keep total page weight
modest, defer/async non-critical scripts, and avoid blocking web fonts (provide a
system-font fallback).

---

## 13. Output format and reuse

- The deliverable produced with this framework is a **polished, implementation-ready
  PRD** for a specific manuscript's website, using clear numbered sections,
  actionable **MUST/SHOULD/MAY** requirements, reusable templates, and filled
  `{{PLACEHOLDERS}}`.
- The document **MUST** be general enough to reuse via a public GitHub repository
  yet specific enough to preserve the scientific, visual, mathematical,
  explanatory, and interactive identity described here.
- Where project details are missing or ambiguous, infer a reasonable default and
  **label it "(Default assumption)"**, exactly as done throughout this document.

---

## Appendix A: Semantic color token system (worked example)

Define one hue per concept, reuse it in equations, curves, sliders, and prose;
pair with bold weight; mute constants to gray. Fill the right column per manuscript.

| Token (role) | Worked-example concept | Worked-example hue | Your manuscript |
| --- | --- | --- | --- |
| `--c-flow` | Blood flow (CBF) / inflow | sky blue `#0ea5e9` | `{{...}}` |
| `--c-metabolism` | Oxygen metabolism (CMRO₂) | red `#dc2626` | `{{...}}` |
| `--c-volume` | Blood volume (CBV) | green `#16a34a` | `{{...}}` |
| `--c-signal-carrier` | Deoxyhemoglobin | indigo `#4338ca` | `{{...}}` |
| `--c-extraction` | Oxygen-extraction fraction | teal `#0d9488` | `{{...}}` |
| `--c-coupling` | Coupling exponent(s) | amber `#b45309` | `{{...}}` |
| `--c-drive` | Neural input | orange `#d97706` | `{{...}}` |
| `--c-time` | Time constants | slate `#64748b` | `{{...}}` |
| `--c-constant` | Calibration constants / scaffolding | muted gray `#94a3b8` | *(keep gray)* |

**Rules:** (1) a symbol and its curve share the hue; (2) constants are always the
muted gray so variables carry the eye; (3) verify each hue against its background
for WCAG AA; (4) never rely on hue alone: pair with bold/label.

---

## Appendix B: Component specification template

```markdown
### {{COMPONENT_NAME}}
- **Purpose:** {{one sentence: what the reader gains}}
- **Content structure:** {{fields / slots and their order}}
- **Visual behavior:** {{layout, color tokens, card/tooltip style, states}}
- **Interaction behavior:** {{hover/focus/drag/expand; what changes; what it teaches}}
- **Accessibility requirements:** {{keyboard, aria, contrast, reduced-motion, non-hover path}}
- **Manuscript placeholders:** {{ {{PLACEHOLDER_1}}, {{PLACEHOLDER_2}}, ... }}
- **Scientific-validity note:** {{how it stays faithful to the manuscript}}
```

---

## Appendix C: Placeholder catalog

`{{TITLE}}` · `{{ONE_LINE_SUMMARY}}` · `{{AUTHORS}}` · `{{STATUS}}` ·
`{{PAPER_URL}}` · `{{DOI}}` · `{{CITATION}}` · `{{BIBTEX}}` ·
`{{RESEARCH_QUESTION}}` · `{{MOTIVATION}}` · `{{METAPHOR}}` · `{{CONCEPTS}}` ·
`{{KEY_FINDING}}` · `{{METHOD}}` · `{{METHODS}}` · `{{EQUATIONS}}` ·
`{{SYMBOLS}}` · `{{TERMS}}` · `{{DEMOS}}` · `{{COMPARISON}}` ·
`{{LIMITATIONS}}` · `{{FURTHER_READING}}` · `{{CODE_URL}}` · `{{DATA_URL}}` ·
`{{SUPP_URL}}` · `{{YEAR}}` · `{{YOUR_NAME}}` · `{{REPO_URL}}` ·
`{{SITE_URL}}` · `{{OG_IMAGE_URL}}`

---

## Appendix D: Mathematical notation design checklist

Adapted from Fred Hohman's *Awesome Mathematical Notation Design* (Color, Layout,
Annotations, Gestalt, Interactivity), with Piotr Migdał's *Equations Explained
Colorfully*, BetterExplained, and Stuart Riffle. Credit this lineage when you use it.

- [ ] **Color:** one meaningful hue per concept, reused everywhere and bridged to figures.
- [ ] **Redundant encoding:** color paired with **bold** weight (color-blind safe).
- [ ] **Annotations:** `\underbrace{…}_{\text{plain language}}` under each sub-expression.
- [ ] **Layout / hierarchy:** mute constants to gray; align related terms to reveal structure.
- [ ] **Gestalt:** group sub-expressions (braces/common region) to chunk the equation.
- [ ] **Interactivity:** per-term hover/focus tooltips with plain-language definitions.
- [ ] **Accessibility:** MathML output *and* unambiguous text fallback (`v^(1/alpha)`, not `v1/alpha`).
- [ ] **Layer separation:** when showing a simplified vs. exact model, label and order them.

---

*End of PRD. This document is intended for public reuse; adapt the placeholders,
keep the scientific-integrity and accessibility requirements.*
