# Print and PDF Contract

Native browser print/save-as-PDF is available in the `read-pdf` and `editable` modes; `read-only` still remains printable by normal browser facilities. These exports cannot promise identical pagination across browsers. A separate build-time reference exporter uses pinned Chromium for reproducible PDFs and validation. Neither path bundles a general-purpose JavaScript PDF drawing engine by default.

PDF export is a primary product output, not a screenshot of the reading view. The aim is faithful reproduction of content and structure in a conventional page layout, with enough white space for annotation.

## Default page design

- A4 default with a selectable US Letter profile.
- Central prose measure of roughly 70–80 characters.
- Larger outer margin reserved for side notes and handwritten annotation.
- Mirrored inner/outer margins for duplex printing.
- Running document title or section context, page number, and optional revision marker.
- Conservative type scale, dark text, and no reliance on colour alone.

Exact dimensions belong in a versioned print theme and must be tested against common office printers' non-printable areas.

## Transformation rules

- All collapsed content expands.
- Hover/focus detail becomes an adjacent note, margin note, footnote, or endnote according to component policy.
- Side notes occupy the outer rail when they fit; otherwise they move immediately after their anchor with a visible note label.
- Links retain visible text; external destinations may be printed in a reference list rather than interrupting prose.
- Internal links remain live in PDF where the engine supports them.
- Table headings repeat across pages; rows avoid splitting unless a row is taller than a page.
- Headings, provision numbers, captions, and note labels are kept with enough following content to remain intelligible.
- Decorative effects are removed. Borders, labels, and hierarchy that carry meaning remain.

## Fidelity acceptance criteria

A release fixture passes only when:

1. **Content parity:** normalized substantive text in HTML and PDF extraction matches after documented normalization; no passage exists only in an interaction layer.
2. **Structural parity:** heading order, provision numbering, lists, table order, note anchors, captions, and cross-references remain identifiable.
3. **No clipping or collision:** automated image comparison and targeted layout assertions detect text outside page boxes, overlapping note/prose regions, or truncated figures.
4. **Stable pagination:** the pinned export environment produces the approved page count and break map for frozen fixtures, subject to an explicit update process.
5. **Search and copy:** text remains searchable and copyable; prose is not rasterized.
6. **Fonts and glyphs:** required fonts are embedded or replaced by an approved metrically compatible stack; missing glyphs fail the build.
7. **Accessibility:** tagged-PDF support is evaluated and documented. Until the export path can guarantee an accessible PDF, the HTML file remains the authoritative accessible edition and the PDF must not be represented otherwise.
8. **Links and outline:** internal links resolve; a PDF outline mirrors the major heading hierarchy when supported by the export engine.

## Test corpus

Fixtures should include:

- a long contract with nested clauses and schedules;
- legislation with amendments, definitions, and long quotations;
- an advice note rich in side notes and citations;
- wide and multi-page tables;
- mixed scripts, diacritics, symbols, and right-to-left passages;
- very long URLs, unbroken identifiers, large images, and notes competing for the same page rail.

Each fixture stores source, normalized model, packaged HTML, expected diagnostics, reference PDF, extracted text, and break-map metadata.

## Reproducibility record

Every PDF export records the document digest, format version, print-theme version, browser engine and version, page profile, locale, and export options. A visible colophon is optional; the machine-readable record is required.

