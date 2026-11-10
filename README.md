# Better Text

Better Text is a proposed single-file, self-contained reading format for serious prose: contracts, legislation, reports, advice, and other documents that need a better screen-reading experience without sacrificing dependable printing and PDF export.

The output is ordinary HTML. It opens offline in a full browser, carries its own presentation and optional behaviour, and is designed to remain useful when scripts are unavailable. The format keeps its component set intentionally small so every document can be rendered as familiar printed prose.

## Design commitments

- **One portable file.** CSS, approved scripts, fonts, and small media assets are embedded; no network access is required.
- **Print is a first-class rendering target.** A generated PDF must preserve all substantive content, hierarchy, numbering, citations, notes, and cross-references.
- **Progressive enhancement.** The document remains readable and printable when JavaScript is disabled.
- **Restrained semantics.** The initial palette is headings, paragraphs, lists, quotations, provisions, figures, tables, call-outs, margin notes, footnotes, citations, and cross-references.
- **Generous page geometry.** The print layout reserves space for side notes and annotation while retaining a familiar central prose column.
- **Inspectable and durable.** Content is HTML, styling is CSS, metadata is embedded JSON, and the conformance rules are public.
- **Safe by default.** The baseline profile contains no remote resources, forms, tracking, storage, or arbitrary executable code.

## Authoring decision

Markdown is the canonical editorial source for the first implementation. It produces reviewable diffs, is easy to validate, and maps predictably to the restrained component model. Word is supported as an ingestion route using a published set of custom styles (for example `Better Text Provision`, `Better Text Side Note`, and `Better Text Callout`). Imports must produce the same normalized intermediate document model as Markdown.

See [ADR 0001](docs/adr/0001-authoring-source.md) for the decision and its review trigger.

## Proposed pipeline

```text
Markdown ──────┐
               ├─> normalized document model ─> validated single HTML file
Word styles ───┘                                  ├─> browser reading view
                                                  └─> print stylesheet ─> PDF
```

The browser rendering and PDF export consume the same semantic HTML. PDF is not a second content representation.

## Repository map

- [`docs/architecture.md`](docs/architecture.md) — system boundaries, build pipeline, safety, and versioning
- [`docs/format-spec.md`](docs/format-spec.md) — initial document profile and semantic component palette
- [`docs/print-and-pdf.md`](docs/print-and-pdf.md) — print contract and fidelity acceptance criteria
- [`docs/editorial-workflow.md`](docs/editorial-workflow.md) — Markdown workflow and Word style bridge
- [`docs/workflow.md`](docs/workflow.md) — issue labels, milestones, and definition of done
- [`docs/issue-backlog.md`](docs/issue-backlog.md) — twelve copy-ready seed issues with dependencies and acceptance criteria
- [`examples/legal-brief.html`](examples/legal-brief.html) — hand-authored proof of the proposed output contract
- [`ROADMAP.md`](ROADMAP.md) — phased delivery plan

## First milestone: executable specification

The first release is not a general-purpose web-page packager. It is a narrow, testable document profile with:

1. a schema for metadata and permitted elements;
2. a Markdown-to-single-HTML reference builder;
3. a print stylesheet and deterministic PDF export;
4. fixture documents that stress numbering, tables, long quotations, notes, and page breaks;
5. automated checks for offline completeness, accessibility, and content parity.

Implementation work is tracked through GitHub issues. Start with the `M0 — Decisions` milestone, then the `M1 — Executable specification` milestone.

## Status

Architecture seed / pre-alpha. The Better Text name is confirmed; the file profile and extension remain provisional until the executable-specification milestone is complete.

