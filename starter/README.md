# Starter template

A working, single-file outreach site that already implements the hard parts of the
[framework](../PRD.md). Copy it, edit one config block, replace the placeholders,
and push.

No build step. No dependencies to install. One HTML file plus a deploy workflow.

## What you get, already working

| Feature | Why it matters | PRD |
| --- | --- | --- |
| **Semantic colour tokens** | One concept, one colour, reused in equations, curves, sliders, and prose | §6.4 |
| **Colour-coded KaTeX equations** | With `\underbrace` annotations and muted constants | §3.2, App. D |
| **Per-term tooltips** | Hover **and keyboard focus and tap**, mirrored into the glossary | §5.4, §6.6 |
| **Accessible equations** | MathML output plus a plain-text fallback with explicit exponents | §3.2, §12.3 |
| **Status badge** | Manuscript status, stated honestly and up front | §9.1 |
| **Pedagogical disclaimer + manuscript-vs-demo table** | The main guard against overinterpretation | §7.10, §9.5 |
| **Demo declaration** | Every demo states its model, parameters, noise, and what it does *not* reproduce | §5.5 |
| **Limitations, glossary, symbol table** | Generated from the same config | §7.7, §7.11 |
| **Flat cards, no accent side bars** | House style | §6.5 |
| **Reduced motion, focus rings, skip link, mobile reflow** | Accessibility is a communication requirement | §12 |
| **Social share card** | Open Graph / Twitter tags + an editable card template, so the link looks right when shared | §7.14 |
| **GitHub Pages workflow** | Push to `main`, the site deploys | §10.2 |

## Quick start

1. Copy the contents of this folder into a new repository (including the hidden
   `.github/` folder).
2. Open `index.html` and edit the **`CONFIG`** block near the bottom. This is the
   single source of truth:

   ```js
   const CONFIG = {
     concepts: {
       drive: {
         symbol: 'u(t)',
         label:  'Drive',
         color:  '#0ea5e9',
         desc:   'The input that pushes the system.',
         units:  'Dimensionless'
       },
       // ... one entry per core concept in your manuscript
     },
     glossary: { 'Steady state': 'The value the response settles to.' },
     muted: '#94a3b8'
   };
   ```

   From this one block the template derives the CSS colour tokens
   (`--c-drive`, ...), the equation colours, the legend, the tooltips, the symbol
   table, and the glossary. **You never repeat a colour anywhere else.**

3. Replace every `{{PLACEHOLDER}}` in the HTML with your manuscript's content.
4. Swap the toy model (a damped first-order system) for your own: the demo block
   and the equations are clearly marked in the source.
5. Work through [`../CHECKLIST.md`](../CHECKLIST.md).
6. In your repository: **Settings > Pages > Source: GitHub Actions**. Push to
   `main` and the site is live.

## Writing an equation

Put the TeX in `data-tex` and a plain-text version inside the element as the
accessible fallback. **Never hard-code a colour in the TeX.**

```html
<div class="eq" role="math"
     data-tex="\frac{d\,\htmlData{term=response}{\boldsymbol{y}}}{dt} =
               \underbrace{\htmlData{term=drive}{\boldsymbol{u}}(t)}_{\htmlData{muted=true}{\text{drive in}}}
               - \underbrace{\htmlData{term=damping}{\boldsymbol{\gamma}}\,\htmlData{term=response}{\boldsymbol{y}}(t)}_{\htmlData{muted=true}{\text{damped away}}}">
  dy/dt = u(t) - gamma*y(t)
</div>
```

- `\htmlData{term=<key>}{...}` marks a **meaningful** symbol. It is coloured from
  `CONFIG.concepts[<key>].color` and gets a tooltip automatically.
- `\htmlData{muted=true}{...}` marks a **calibration constant** or an annotation
  label. It is greyed so the real variables carry the eye.
- Use `\boldsymbol{}` so colour is paired with weight (colour-blind safe).
- The fallback text uses `^( )` for exponents: `y^(2)`, never `y2`.

## The share card (how the link looks when shared)

`index.html` already includes the Open Graph and Twitter meta tags. Two steps make
them work:

1. **Make the image.** Edit [`assets/social-card.svg`](assets/social-card.svg)
   (title, summary, status, concept chips, colours to match your `CONFIG`), then
   rasterise it:

   ```bash
   npx --yes sharp-cli -i assets/social-card.svg -o assets/social-card.png \
     --density 144 resize 1200 630
   ```

2. **Point the tags at it.** In `index.html`, set `{{OG_IMAGE_URL}}` and
   `{{SITE_URL}}` to **absolute** URLs (e.g.
   `https://yourname.github.io/yourrepo/assets/social-card.png`). Relative URLs do
   not work for social cards.

Rules of thumb: 1200×630, large high-contrast text (it is seen as a thumbnail), and
nothing that is not also on the page. For a **GitHub repository** preview, upload
the PNG under **Settings → Social preview** (repo previews are not read from files).
Social platforms cache cards, so use their debuggers to re-scrape after a change.

## Local preview

Any static server works:

```bash
python3 -m http.server 8000
# or
npx --yes serve .
```

## Before you publish

- [ ] Every `{{PLACEHOLDER}}` is gone.
- [ ] The status badge matches reality (`preprint`, `under review`, `published`).
- [ ] The manuscript-vs-demo table is filled in truthfully.
- [ ] Each demo declares its model, parameters, noise, and what it does not reproduce.
- [ ] Every claim is traceable to the manuscript.
- [ ] Tab through the page: equations, sliders, and tooltips are all reachable.
- [ ] Reviewed by a domain expert **and** a non-expert.
