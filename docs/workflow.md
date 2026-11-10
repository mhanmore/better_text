# GitHub Work Workflow

## Milestones

- **M0 — Decisions:** scope, licensing, security, naming, and semantic palette.
- **M1 — Executable specification:** schemas, builder, packaging, print theme, exporter, and fixtures.
- **M2 — Editorial bridge:** Word template/importer and validation experience.
- **M3 — Reader hardening:** interaction, accessibility, compatibility, integrity, and v0.1 publication.

## Labels

Use one `type`, one or more `area`, and optionally one `priority` label.

- `type:decision`, `type:feature`, `type:test`, `type:docs`, `type:research`
- `area:format`, `area:authoring`, `area:reader`, `area:print-pdf`, `area:accessibility`, `area:security`, `area:tooling`
- `priority:p0`, `priority:p1`, `priority:p2`
- `status:blocked`, `status:needs-design`, `good first issue`

## Issue shape

Every implementation issue should state:

- the reader or author outcome;
- scope and non-goals;
- acceptance criteria that can be observed or tested;
- affected fixtures and compatibility risks;
- dependencies and follow-up work.

## Delivery flow

1. Decisions begin as an issue labelled `type:decision` and conclude in an ADR.
2. Features start with a fixture or concrete example before implementation.
3. A pull request links its issue and includes generated HTML/PDF evidence when rendering changes.
4. Format changes update the specification, validator, fixtures, and migration notes together.
5. A milestone closes only when its acceptance checklist and reference fixtures pass in the pinned export environment.

## Definition of done

- behaviour is specified and implemented;
- automated tests cover valid, invalid, screen, and print behaviour as applicable;
- no substantive content depends on JavaScript;
- accessibility and keyboard behaviour have been checked;
- offline validation reports zero network dependencies;
- PDF content-parity and layout checks pass for affected fixtures;
- documentation and change notes are updated;
- failure messages tell an author how to correct the source.

## Initial issue sequence

The first issues should be created in this order:

1. Confirm the profile identifier and file extension for Better Text.
2. Choose licensing for specification, code, and examples.
3. Approve v0 threat model and scripting policy.
4. Freeze the v0 semantic component palette.
5. Define the normalized document model and metadata schema.
6. Specify Markdown directives and source diagnostics.
7. Implement single-file packaging and offline validation.
8. Implement print theme and deterministic PDF export.
9. Build the legal-document fidelity corpus and parity checks.
10. Define and test the Word custom-style template and importer.
11. Accessibility and keyboard conformance pass.
12. Publish the v0.1 executable specification.

