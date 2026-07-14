# Examples

Real projects built with this framework. Each example should record what a future
adapter needs: the concept→color map, the demo assumptions, and links to the live
site and the manuscript.

## Worked example: neurovascular modeling companion site

An interactive companion site for a peer-reviewed neuroimaging manuscript on how
neurovascular coupling impairments reshape BOLD-based functional connectivity.
This project is the source from which the framework was distilled.

| Field | Value |
| --- | --- |
| Manuscript | Archila-Meléndez, Sorg & Preibisch, *NeuroImage* 218:116871 (2020) |
| DOI | https://doi.org/10.1016/j.neuroimage.2020.116871 |
| Live site | https://virtualmarioe.github.io/neurovascular_modeling/ |
| Site source | https://github.com/virtualmarioe/neurovascular_modeling |
| Data & code | Zenodo archive; authors' GitLab repository |
| Status | Published (peer reviewed) |

### Patterns this project contributed to the framework

- **Primer-first ramp:** a narrated "Meet the balloon" animation, the picture before the equations.
- **Semantic color system:** one hue per physiological concept, bridged from equations to curves to sliders (see `templates/color-tokens.md`).
- **Notation design:** color-coded KaTeX with `\underbrace` annotations, muted constants, and per-term hover tooltips (PRD Appendix D).
- **Model-layer separation:** MR physics → classic model → the paper's adjusted model → the demo's simplified engine, each labeled and ordered.
- **Paper-vs-demo comparison table:** a permanent table contrasting the peer-reviewed simulation with the browser demo, to prevent overinterpretation.
- **Honest caveats:** pedagogical-tool disclaimer; correlation values framed as model- and noise-dependent rather than predictions.
- **Card style:** homogeneous light backgrounds, no accent side bars.

### Adding your own example

Copy this section, fill in the table, and list the patterns your project
contributed or adapted. Pull requests welcome (see `CONTRIBUTING.md`).
