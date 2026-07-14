# Semantic color tokens

One hue per scientific concept, reused everywhere: equations, curves, sliders,
legends, and prose. See PRD §6.4 and Appendix A.

## Rules

1. A symbol and its curve **share the hue**.
2. Pair color with **bold weight** (redundant encoding) so it survives color-vision deficiency.
3. Calibration constants and scaffolding are **muted gray** so the variables carry the eye.
4. Check every hue against its background for **WCAG AA** contrast.
5. Never encode meaning by hue alone: add a label, weight, or shape.

## Your manuscript's tokens

| Token (role) | Concept in your manuscript | Hue | Used in (equations / curves / sliders) |
| --- | --- | --- | --- |
| `--c-concept-1` | `{{CONCEPT_1}}` | `{{#HEX}}` | `{{...}}` |
| `--c-concept-2` | `{{CONCEPT_2}}` | `{{#HEX}}` | `{{...}}` |
| `--c-concept-3` | `{{CONCEPT_3}}` | `{{#HEX}}` | `{{...}}` |
| `--c-drive` | `{{INPUT_OR_DRIVER}}` | `{{#HEX}}` | `{{...}}` |
| `--c-time` | Time constants | `#64748b` (slate) | `{{...}}` |
| `--c-constant` | Calibration constants | `#94a3b8` (muted gray) | all equations |

## Worked example (neuroimaging companion site)

| Concept | Hue |
| --- | --- |
| Blood flow (CBF) / inflow | sky blue `#0ea5e9` |
| Oxygen metabolism (CMRO₂) | red `#dc2626` |
| Blood volume (CBV) | green `#16a34a` |
| Deoxyhemoglobin | indigo `#4338ca` |
| Oxygen-extraction fraction | teal `#0d9488` |
| Coupling exponents | amber `#b45309` |
| Neural input | orange `#d97706` |
| Time constants | slate `#64748b` |
| Calibration constants | muted gray `#94a3b8` |
