# Manuscript → Website Adaptation Checklist

Copy this file into your project and check items off as you go. It operationalizes
[`PRD.md`](PRD.md). Items map to PRD sections in parentheses.

## 1. Extract the scientific spine (§8.1)
- [ ] Central **research question** in one plain sentence.
- [ ] **Motivation** (why it matters) in one plain sentence.
- [ ] Single **headline finding** in one plain sentence.
- [ ] **Manuscript status**: preprint / under review / accepted / published (+ DOI, date, version). (§9.1)

## 2. Inventory the science (§8.1)
- [ ] Methods (in a phrase, and in full for the expert layer).
- [ ] Key **equations / mathematical structures** to show.
- [ ] **Datasets** and how to link/share them.
- [ ] **Key figures** to recreate (prefer inline SVG).
- [ ] **Parameters** and their values/units.
- [ ] **Assumptions** and **limitations** (these are first-class content). (§3.2)
- [ ] Broader **implications**, bounded by what the paper supports. (§9.3)

## 3. Design the explanation (§4)
- [ ] Pick the **central metaphor / entry image** for beginners.
- [ ] Draft the **ramp**: motivation → intuition → question → mechanism → interaction → figures → math → interpretation → limitations → citations.
- [ ] Define **beginner / intermediate / expert** content for each core concept.
- [ ] Ensure every technical section has a conceptual summary that links to it.

## 4. Build the visual system (§6, Appendix A)
- [ ] **Semantic color table**: one hue per concept; fill Appendix A.
- [ ] Bridge each **equation color to its figure/curve color**.
- [ ] Mute **constants/scaffolding** to gray.
- [ ] Set typography scale; body ≥ 16 px; system-font fallback.
- [ ] Cards/callouts: **homogeneous light background, no accent side bars**.
- [ ] Define the **tooltip** style (hover + focus/tap; concept-colored).
- [ ] (Optional house style) no em dashes in body copy.

## 5. Design the notation (§3.2, Appendix D)
- [ ] Color + **bold** on meaningful terms (color-blind safe).
- [ ] `\underbrace{}` **annotations** under sub-expressions.
- [ ] Constants muted; related terms aligned.
- [ ] Per-term **hover/focus tooltips**.
- [ ] **Accessible fallback**: MathML + unambiguous text (`v^(1/alpha)`).
- [ ] If showing simplified vs. exact models, **label and order the layers**. (§3.4)

## 6. Choose interactions (§5)
- [ ] Each interaction lets the reader **test a paper relationship** (not decoration).
- [ ] Sliders/controls **color-matched** to concepts; keyboard-operable.
- [ ] **Live derived metric** tied to the paper's headline statistic (where relevant).
- [ ] State each demo's **model, parameters, noise, seed, and caveats** on the page.
- [ ] Demo outputs consistent with the manuscript's **direction of effect**.
- [ ] Numbers labeled **model/noise-dependent**, not predictions (unless truly reproducing the paper).
- [ ] Add a **paper-vs-demo comparison table**. (§7.10)

## 7. Responsible communication (§9)
- [ ] **Status badge** in hero and near citation.
- [ ] Uncertainty line for non-peer-reviewed work.
- [ ] Hedged verbs for interpretation; no causal/clinical overreach.
- [ ] Pedagogical-tool **disclaimer** if demos are simplified.
- [ ] Links to **manuscript, data, code, supplementary materials, version history**.

## 8. Accessibility & performance (§12)
- [ ] Full **keyboard** operation + visible focus.
- [ ] **WCAG AA** contrast; meaning never by color alone.
- [ ] Semantic HTML; MathML; figures have `aria-label`; hover content mirrored in text.
- [ ] **`prefers-reduced-motion`** honored.
- [ ] **Mobile**: single-column reflow, scrollable equations, touch-usable controls (test ~360 px).
- [ ] **Graceful degradation** if JS fails; fast first paint.

## 9. Repository & publishing (§10)
- [ ] `README.md` with status badge + links; `LICENSE`; `CITATION.cff`.
- [ ] Record the **concept→color map** and **demo assumptions** in `docs/`.
- [ ] Attribution to this framework and the notation-design lineage.

## 10. Final review
- [ ] Reviewed by a **domain expert** for accuracy.
- [ ] Reviewed by a **non-expert** for accessibility of the explanation.
- [ ] Every claim traceable to the manuscript or a cited source.
