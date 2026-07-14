# Component specification template

Copy this block for each custom component. See PRD §7 and Appendix B.

---

### {{COMPONENT_NAME}}

- **Purpose:** {{one sentence: what the reader gains that they could not get otherwise}}
- **Content structure:** {{fields / slots and their order}}
- **Visual behavior:** {{layout, color tokens used, card or tooltip style, states}}
- **Interaction behavior:** {{hover / focus / drag / expand; what changes; what it teaches}}
- **Accessibility requirements:** {{keyboard path, aria, contrast, reduced-motion, non-hover fallback}}
- **Manuscript placeholders:** {{ {{PLACEHOLDER_1}}, {{PLACEHOLDER_2}} }}
- **Scientific-validity note:** {{how this stays faithful to the manuscript; what it simplifies and where that is disclosed}}

---

## Reminders

- If the interaction does not change what the reader understands, remove it (PRD §5.1).
- Anything shown only on hover must also exist in text (glossary, table, or caption) (PRD §5.4).
- Simplifications must be disclosed at or near the control (PRD §5.3).
