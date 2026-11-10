# Contributing

The project is currently architecture-first. Changes should make the carrier more dependable for authors and readers without expanding it into a general web-application package.

## Before opening a change

1. Link an issue that states the outcome and acceptance criteria.
2. Add or identify a representative fixture.
3. For format changes, update the specification and record compatibility consequences.
4. For rendering changes, compare both the screen document and the exported PDF.

## Principles reviewers will enforce

- Substantive content exists in the semantic HTML, not only in script state.
- The file works offline and does not make automatic network requests.
- Keyboard, touch, focus, no-script, and print treatments exist for every interaction.
- Unsupported source content produces a useful diagnostic rather than silent loss.
- Print/PDF evidence is required when pagination, notes, tables, fonts, or page geometry can change.

## Decision records

Use an ADR in `docs/adr/` for durable architecture and editorial decisions. A decision issue should describe the context, options, criteria, and compatibility consequences before the ADR is accepted.

