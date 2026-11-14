# Reuse, Bundling and Three Export Modes

Status: proposed technical direction; library choices require a measured proof of concept.

## Goals

Better Text packages serious prose as one offline HTML file, with three capability profiles:

| Profile | Included | Intentionally excluded |
| --- | --- | --- |
| Read-only | Semantic rendered HTML, styling, accessible navigation, print stylesheet and approved minimal viewer behaviour | Canonical Markdown, editing runtime and dedicated PDF action |
| Read + PDF | All read-only content plus browser-native print/save-as-PDF controls | Full in-browser PDF renderer; editing |
| Full editable | All read + PDF capabilities plus embedded canonical Markdown, syntax-aware text editing, local parser/render and self-contained HTML export | WYSIWYG, arbitrary executable MDX/JSX, server dependency |

Read-only is still natively printable; the dedicated PDF control distinguishes the middle profile. PDF equivalence across browser engines is not guaranteed.

## Reuse candidates

| Need | Candidate | Decision condition |
| --- | --- | --- |
| Base Markdown and GFM | Selected modular MyST parser or lighter CommonMark/GFM parser | Parser fidelity, tree-shaken cost, auditability, offline browser operation |
| Directive syntax and semantics | Selected MyST directive components, with a Better Text allowlist | Colon-fence compatibility, unknown directives rejected, no code evaluation |
| Normalized AST / semantic transforms | Selected MyST spec/transform packages where appropriate | Stable IDs, numbering, citations and cross-references meet legal-document fixtures |
| Markdown editing | CodeMirror 6, loaded only in editable profile | Lightweight configuration, syntax help without WYSIWYG, keyboard/touch accessibility |
| Rendering | Adapt existing transforms where viable; Better Text-controlled semantic HTML/CSS | No-script parity, predictable print layout and small bundle |
| PDF | Native browser print; separate pinned-Chromium reference export | Test page fidelity, text extraction, repeatability and browser variance |

MyST (https://github.com/jupyter-book/mystmd) is an architectural and package-level reuse candidate, **not** a decision to bundle its whole publisher. CodeMirror 6 (https://codemirror.net/) is the editor candidate. Check exact package versions, licences and transitive notices before shipping.

## Canonical content and HTML output

- Source syntax: CommonMark/GFM and a limited, specified MyST-compatible colon-fenced directive grammar. Standard source extension: `.md`; no MDX runtime.
- The normalized document model drives all three outputs. Substantive rendered HTML is complete even with JavaScript disabled.
- In editable packages only, embedded inert Markdown is **the authoritative source**; rendered HTML is a generated snapshot, not an independent editable source.
- The editor works on Markdown text and rebuilds the view locally. Saving produces a new standalone HTML download. Do not promise overwrite-in-place, particularly in iOS browsers.
- Export checks source/rendered parity, stable IDs, metadata, size and network independence.
- Document images are independently size-budgeted; font embedding is optional and licence-dependent.

## Indicative size budgets, not measured results

For modest prose documents without large images:

- Read-only: approximately 50–200 KB.
- Read + PDF: approximately 60–250 KB using browser-native printing.
- Full editable: approximately 350 KB–1.2 MB with a lean parser/editor and limited font subsets; provisionally aim for **750 KB–1 MB**.
- Adding a complete embedded JavaScript PDF engine could take the editable package towards 0.8–2.5 MB or beyond. Avoid this unless justified.

These are planning ranges for uncompressed HTML, not promised limits. Large images, fonts and a heavyweight MyST bundle can substantially increase them.

## Proof-of-concept gates

1. Build a legal-document fixture featuring nested provisions, notes, citations, cross-references, tables and long quotations in the proposed directive dialect.
2. Bundle two candidate pipelines (selected MyST modules versus a lighter Markdown/GFM parser with directive extension) and measure raw, minified and gzip transfer sizes separately.
3. Run all three resulting HTML profiles from `file://` with networking blocked, including Safari/iOS and Chromium.
4. Verify safe handling of untrusted Markdown, HTML injection, SVG, links, nested directives and malformed metadata under the chosen CSP.
5. Confirm print parity and default native PDF output; separately test pinned-browser pagination and content parity.
6. In editable mode, change Markdown, rebuild the view, download a new standalone HTML file, reopen it offline, and compare content/IDs.
7. Capture third-party licences, attributions and precise bundle costs; reject components that violate the size, offline or safety targets.

## Open decisions

- Whether selected MyST packages are affordable in the browser, or should be used only in the build CLI.
- Exact directive allowlist and permitted argument types.
- Which derived assets, e.g. citation records, are stored in editable files rather than recomputed.
- The supported iOS file-export UX and expected fallback.
- Specific versions and reproducibility policy for in-browser parser/renderer versus build-time reference implementation.
