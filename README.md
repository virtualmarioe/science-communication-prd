# Interactive Science-Communication Website Framework

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.21356399-1682D4)](https://doi.org/10.5281/zenodo.21356399)
[![Docs: CC BY 4.0](https://img.shields.io/badge/Docs-CC%20BY%204.0-blue)](LICENSE)
[![Code: MIT](https://img.shields.io/badge/Code-MIT-green)](LICENSE)

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

## How to cite

If this framework helped you build an outreach site, please cite it:

> Archila-Meléndez, M. E. (2026). *Interactive Science-Communication Website
> Framework (PRD)* (v1.0.0). Zenodo. https://doi.org/10.5281/zenodo.21356399

```bibtex
@software{ArchilaMelendez2026scicommprd,
  author    = {Archila-Mel{\'e}ndez, Mario E.},
  title     = {Interactive Science-Communication Website Framework (PRD)},
  year      = {2026},
  version   = {v1.0.0},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.21356399},
  url       = {https://doi.org/10.5281/zenodo.21356399}
}
```

### Which DOI is which

Zenodo mints **two** DOIs. They are both correct; they point at different things.

| DOI | Resolves to | Use it for |
| --- | --- | --- |
| [`10.5281/zenodo.21356399`](https://doi.org/10.5281/zenodo.21356399) | **All versions**, always redirecting to the newest release | The badge above, the citation, `CITATION.cff`. **Cite this one.** |
| [`10.5281/zenodo.21356400`](https://doi.org/10.5281/zenodo.21356400) | **`v1.0.0` only**, a frozen snapshot | Reproducing exactly this version |

The Zenodo record page prominently shows the *version* DOI (`...400`), which is why
it differs from the badge. That is expected. The badge deliberately uses the
concept DOI (`...399`) so that a citation made today still resolves correctly after
`v1.1.0` is released, instead of pointing at a stale version forever.

Machine-readable metadata is in [`CITATION.cff`](CITATION.cff).

## Reuse, attribution, and license

- **License:** documentation under **CC BY 4.0**; code samples under **MIT**. See [`LICENSE`](LICENSE).
- **Attribution:** keep credit to this framework, and to the notation-design lineage (Fred Hohman's *Awesome Mathematical Notation Design*; Piotr Migdał's *Equations Explained Colorfully*; BetterExplained; Stuart Riffle) where the notation rules are used.
- **Responsible reuse:** forks must preserve the scientific-integrity, honest-caveat, and accessibility requirements; they are the point of the framework.

Contributions welcome: see [`CONTRIBUTING.md`](CONTRIBUTING.md).
