# Contributing

Thanks for helping improve this framework. It exists so that other scientists can
turn manuscripts into accessible, accurate, interactive outreach websites, so the
bar for changes is: **does this make the resulting websites more scientifically
honest, more understandable, or more accessible?**

## Ways to contribute

- **Report a gap.** Open an issue if a rule is ambiguous, missing, or fails for
  your field. Say which manuscript type exposed the gap.
- **Improve a rule.** Propose sharper wording, a better default, or evidence that
  a default is wrong.
- **Add an example.** A real project built with the framework, added under
  `examples/`, is the most valuable contribution. Include the concept→color map,
  the demo assumptions, and a link to the live site and the manuscript.
- **Add a component spec.** Use `templates/component-spec.md`.

## Non-negotiables

Changes **must not** weaken these, which are the point of the framework:

1. **Scientific integrity** (PRD §3): claims traceable to the manuscript; intuition,
   interpretation, results, and limitations kept distinct.
2. **Responsible communication** (PRD §9): manuscript status labeled; no overstated
   causal/clinical claims; simplified demos clearly separated from the peer-reviewed
   analysis; links to data and code.
3. **Accessibility** (PRD §12): keyboard operation, WCAG AA contrast, screen-reader
   semantics, reduced-motion support, mobile readability. These are communication
   requirements, not polish.

## Style

- Requirements use **MUST / SHOULD / MAY** (RFC 2119 sense).
- Inferred defaults are labeled **(Default assumption)**.
- Manuscript-specific slots use `{{DOUBLE_BRACES}}`.
- Keep the document domain-agnostic; put field-specific material in `examples/`.
- House style: no em dashes in body copy (use commas, parentheses, or a colon).

## Pull requests

1. Keep PRs focused on one rule, section, or example.
2. Explain the problem your change solves, not just the change.
3. If you alter a default, say why the old default failed.
4. Update `CHECKLIST.md` if your change adds or removes an actionable step.

## Code of conduct

Be constructive and assume good faith. Critique the framework, not the person.
