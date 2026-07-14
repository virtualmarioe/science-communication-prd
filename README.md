# Interactive Science-Communication Website Framework

A reusable **Product Requirements Document (PRD)** and design framework for turning
a scientific manuscript into an **accessible, precise, visually coherent, and
interactive outreach website**.

Take a new manuscript, swap in the manuscript-specific science, and use this
framework to plan a site that a curious non-expert can enter and an expert can
trust, without diluting the science.

> Works for **preprints, and peer-reviewed manuscripts**, in
> any field. The worked example throughout is a neuroimaging companion site, but
> the rules (notation design, layered explanation, honest caveats,
> interaction-for-understanding) are domain-agnostic.

## What's here

| File | Purpose |
| --- | --- |
| [`PRD.md`](PRD.md) | The full framework: 13 sections + appendices (color tokens, component template, placeholders, notation checklist). |
| [`CHECKLIST.md`](CHECKLIST.md) | A runnable adaptation checklist to go from manuscript → website plan. |
| [`templates/`](templates/) | Blank component spec, color-token table, and content-model plan. |
| [`examples/`](examples/) | Notes and links for real projects built with the framework. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to improve the framework, and the non-negotiables. |
| [`LICENSE`](LICENSE) | CC BY 4.0 for documentation; MIT for code samples. |
| [`CITATION.cff`](CITATION.cff) | Machine-readable citation. |

## Quick start

1. Read [`PRD.md`](PRD.md) once end to end.
2. Copy [`CHECKLIST.md`](CHECKLIST.md) into your project and work through it with the manuscript open.
3. Build your **semantic color table** (PRD Appendix A): one hue per concept, reused everywhere.
4. Design your equations with the **notation checklist** (PRD Appendix D).
5. Fill the **content model** (PRD §11) and its `{{placeholders}}`.
6. Apply the **responsible-communication** rules (PRD §9): status badge, hedging, links.
7. Meet the **accessibility & performance** budgets (PRD §12).
8. Review with a domain expert *and* a non-expert before publishing.

## Core principles (the short version)

- **Layer, don't dilute.** Intuition → mechanism → formalism, all present at once via progressive disclosure.
- **Color carries meaning.** One hue per concept, reused in equations, curves, sliders, and prose; constants muted to gray; color paired with bold for color-blind safety.
- **Interactivity teaches.** Every control must change what the reader understands, and must stay faithful to the manuscript's direction of effect.
- **Be honest.** Label manuscript status, hedge preliminary claims, separate the toy demo from the peer-reviewed analysis, and link to data and code.
- **Access is communication.** Keyboard, contrast, screen readers, reduced motion, and mobile readability are requirements, not polish.

## Reuse, attribution, and license

- **License (default):** documentation under **CC BY 4.0**; example code under a permissive license (e.g. MIT). Set this explicitly in `LICENSE`.
- **Attribution:** keep credit to this framework, and to the notation-design lineage (Fred Hohman's *Awesome Mathematical Notation Design*; Piotr Migdał's *Equations Explained Colorfully*; BetterExplained; Stuart Riffle) where the notation rules are used.
- **Responsible reuse:** forks must preserve the scientific-integrity, honest-caveat, and accessibility requirements; they are the point of the framework.

Contributions welcome: see [`CONTRIBUTING.md`](CONTRIBUTING.md).
