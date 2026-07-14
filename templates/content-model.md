# Content model plan

Fill one row per section before building. See PRD §11.

| # | Section | Role | Reader level | Your content |
| --- | --- | --- | --- | --- |
| 1 | Landing / hero | Orient; status; actions | All | `{{TITLE}}`, `{{STATUS}}`, `{{PAPER_URL}}` |
| 2 | Scientific motivation | Why this matters | Beginner | `{{MOTIVATION}}` |
| 3 | Conceptual background | Mental model + metaphor | Beginner → Intermediate | `{{METAPHOR}}`, `{{CONCEPTS}}` |
| 4 | Core result | The headline finding | All | `{{KEY_FINDING}}` |
| 5 | Interactive exploration | Test the relationships | Intermediate | `{{DEMOS}}` |
| 6 | Mathematical details | Formalism, layered | Expert | `{{EQUATIONS}}`, `{{SYMBOLS}}` |
| 7 | Manuscript connection | Map demo ↔ paper; methods | Intermediate → Expert | `{{METHODS}}`, `{{COMPARISON}}` |
| 8 | Limitations | What it does not show | All | `{{LIMITATIONS}}` |
| 9 | Glossary & symbols | Reference | All | `{{TERMS}}`, `{{SYMBOLS}}` |
| 10 | Citations & reproducibility | Cite; data; code | All | `{{CITATION}}`, `{{CODE_URL}}`, `{{DATA_URL}}` |
| 11 | Further reading | Context; next steps | All | `{{FURTHER_READING}}` |

## The three sentences to write first

- **Research question:** `{{RESEARCH_QUESTION}}`
- **Motivation:** `{{MOTIVATION}}`
- **Headline finding:** `{{KEY_FINDING}}`

If you cannot write these in plain language, the site is not ready to build.

## Demo declaration (repeat per demo)

- **Illustrates (manuscript concept/figure):** `{{...}}`
- **Model actually computed:** `{{...}}`
- **Parameters / seed:** `{{...}}`
- **Noise model:** `{{...}}`
- **What it does NOT reproduce:** `{{...}}`
