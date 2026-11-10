# Initial GitHub Issue Backlog

These are the copy-ready seed issues. Create milestones and labels from [`workflow.md`](workflow.md), then add these issues in order. Dependencies are deliberately explicit so the list can be transferred into GitHub Projects without reinterpretation.

## 1. Confirm the Better Text profile identifier and file extension

**Labels:** `type:decision`, `area:format`, `priority:p0`  
**Milestone:** M0 — Decisions

**Outcome:** The confirmed Better Text name has stable identifiers that are safe to encode in files and metadata.

**Acceptance criteria:**

- [x] Repository name is `better_text` and the human-readable format name is Better Text.
- [ ] HTML profile identifier and version attribute are selected.
- [ ] v0 uses `.html` or a documented compound extension with tested operating-system behaviour.
- [ ] ADR records rejected options and migration consequences.

## 2. Choose licensing for specification, code, and examples

**Labels:** `type:decision`, `area:tooling`, `priority:p0`  
**Milestone:** M0 — Decisions

**Outcome:** Contributors and implementers know what they may reuse.

**Acceptance criteria:**

- [ ] Code, specification text, and sample-content licensing are decided separately where appropriate.
- [ ] `LICENSE` and any required notices are committed.
- [ ] Contribution terms are documented.

## 3. Approve the v0 threat model and scripting policy

**Labels:** `type:decision`, `area:security`, `area:reader`, `priority:p0`  
**Milestone:** M0 — Decisions

**Outcome:** Opening a conforming file offline has a clear and testable security boundary.

**Acceptance criteria:**

- [ ] Allowed and prohibited browser capabilities are enumerated.
- [ ] Network isolation and Content Security Policy requirements are testable.
- [ ] Author-provided scripts and inline event handlers are rejected.
- [ ] Enhanced and no-script profiles have explicit conformance rules.
- [ ] Threats from links, embedded SVG, fonts, media, and oversized data are covered.

## 4. Freeze the v0 semantic component palette

**Labels:** `type:decision`, `area:format`, `area:accessibility`, `priority:p0`  
**Milestone:** M0 — Decisions  
**Depends on:** #3

**Outcome:** Every permitted component has stable semantics and screen, print, fallback, and accessibility treatments.

**Acceptance criteria:**

- [ ] Component list in `docs/format-spec.md` is accepted or revised.
- [ ] Nesting rules and required attributes are specified.
- [ ] Hover behaviour has focus, touch, no-script, and print equivalents.
- [ ] Excluded HTML features are listed.

## 5. Define the normalized document model and metadata schema

**Labels:** `type:feature`, `area:format`, `area:tooling`, `priority:p0`  
**Milestone:** M1 — Executable specification  
**Depends on:** #4

**Outcome:** Source adapters produce one typed, validated representation.

**Acceptance criteria:**

- [ ] Schema covers every v0 component, stable IDs, source locations, language, numbering, and provenance.
- [ ] Required and recommended carrier metadata are machine-validated.
- [ ] Valid and invalid fixture models are committed.
- [ ] Unknown nodes fail with source-oriented diagnostics.

## 6. Specify Markdown directives and source diagnostics

**Labels:** `type:feature`, `area:authoring`, `area:format`, `priority:p0`  
**Milestone:** M1 — Executable specification  
**Depends on:** #5

**Outcome:** Authors can express the full v0 model in readable Markdown.

**Acceptance criteria:**

- [ ] Directive grammar, escaping, nesting, and ID generation are specified.
- [ ] Parser emits the normalized model and source locations.
- [ ] Duplicate IDs, unresolved references, invalid nesting, and missing labels have actionable errors.
- [ ] Representative legal prose fixture parses without HTML escape hatches.

## 7. Implement single-file packaging and offline validation

**Labels:** `type:feature`, `area:tooling`, `area:security`, `priority:p0`  
**Milestone:** M1 — Executable specification  
**Depends on:** #3, #5

**Outcome:** A validated model becomes one portable HTML file that makes no automatic network requests.

**Acceptance criteria:**

- [ ] CSS, approved reader script, and assets are embedded.
- [ ] Semantic HTML remains complete with scripts disabled.
- [ ] Validator rejects remote resource dependencies, event handlers, forms, frames, storage, and prohibited APIs.
- [ ] Build metadata contains profile, builder, source digest, and packaged digest.
- [ ] Output opens successfully from a local filesystem path in supported browsers.

## 8. Implement print theme and deterministic PDF export

**Labels:** `type:feature`, `area:print-pdf`, `priority:p0`  
**Milestone:** M1 — Executable specification  
**Depends on:** #7

**Outcome:** The same semantic file produces a familiar, annotation-friendly PDF without losing content or structure.

**Acceptance criteria:**

- [ ] Versioned A4 theme implements mirrored generous margins and a side-note rail.
- [ ] US Letter profile is selectable.
- [ ] Collapsed and hover-only details receive complete print treatments.
- [ ] Pinned browser export records a reproducibility manifest.
- [ ] Links, headings, lists, tables, captions, provision numbers, and notes meet `docs/print-and-pdf.md`.

## 9. Build the legal-document fidelity corpus and parity checks

**Labels:** `type:test`, `area:print-pdf`, `area:format`, `priority:p0`  
**Milestone:** M1 — Executable specification  
**Depends on:** #6, #8

**Outcome:** Content loss, clipping, collisions, and unintended pagination changes fail automated checks.

**Acceptance criteria:**

- [ ] Corpus covers contracts, legislation, advice, nested numbering, dense notes, wide tables, mixed scripts, and pathological content.
- [ ] HTML/PDF normalized-text parity is checked.
- [ ] Page boxes, font embedding, glyph coverage, link targets, and outline are checked where supported.
- [ ] Reference pagination changes require an explicit review artifact.

## 10. Define and test the Word custom-style template and importer

**Labels:** `type:feature`, `area:authoring`, `priority:p1`  
**Milestone:** M2 — Editorial bridge  
**Depends on:** #5

**Outcome:** Word-centric authors can enter the pipeline without silent semantic loss.

**Acceptance criteria:**

- [ ] Template implements the style map in `docs/editorial-workflow.md`.
- [ ] Importer maps native tables, links, images, notes, and supported styles to the normalized model.
- [ ] Unresolved tracked changes fail by default; comments and unsupported formatting are reported.
- [ ] Three representative documents are imported and compared with hand-authored reference models.

## 11. Complete the accessibility and keyboard conformance pass

**Labels:** `type:test`, `area:accessibility`, `area:reader`, `priority:p0`  
**Milestone:** M3 — Reader hardening  
**Depends on:** #7, #8

**Outcome:** The HTML edition is operable and understandable across keyboard, touch, and assistive-technology use.

**Acceptance criteria:**

- [ ] Heading, landmark, link, table, figure, note, and disclosure semantics are tested.
- [ ] Focus order and focus visibility pass in supported browsers.
- [ ] Popovers and collapsible content have equivalent touch, no-script, and print access.
- [ ] Zoom, reflow, contrast, reduced-motion, and forced-colour checks are documented.
- [ ] The accessibility status of exported PDF is stated accurately.

## 12. Publish the v0.1 executable specification

**Labels:** `type:docs`, `area:format`, `area:tooling`, `priority:p0`  
**Milestone:** M3 — Reader hardening  
**Depends on:** #1–#11

**Outcome:** Independent implementers can build and test a compatible core document.

**Acceptance criteria:**

- [ ] Format, schemas, conformance classes, and security profile are versioned and published.
- [ ] Reference builder, validator, reader assets, PDF exporter, and fixtures are released together.
- [ ] Compatibility matrix and known limitations are published.
- [ ] Migration and change-control process is documented.

