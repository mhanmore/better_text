# Initial Format Profile

This document defines the proposed v0 semantic surface. It is intentionally narrower than HTML.

## Document structure

A document contains metadata, optional front matter, and one ordered main body. Headings form a valid hierarchy. Every addressable section and provision receives a stable ID. Language is declared at document and, when necessary, span level.

Required metadata:

- format profile and version;
- document title;
- primary language;
- build timestamp and builder version;
- source digest and packaged-content digest.

Recommended metadata:

- subtitle, author or issuing body, document date, jurisdiction, status, revision, and canonical identifier.

## Semantic component palette

| Component | HTML basis | Screen treatment | Print treatment |
| --- | --- | --- | --- |
| Section | `section`, headings | navigable hierarchy | controlled breaks and running context |
| Paragraph | `p` | readable measure | conventional prose |
| Ordered/unordered list | `ol`, `ul` | native list | preserved numbering and indentation |
| Provision | numbered `section` | deep-linkable number and text | number kept with opening lines |
| Long quotation | `blockquote` | optionally collapsible after a visible lead | always fully expanded |
| Call-out | `aside` with role | inset panel | bordered block in prose flow |
| Margin note | `aside` linked to anchor | side rail where space permits | outer margin or inline fallback |
| Footnote/endnote | linked note pair | popover plus note list | footnote or endnote policy, never omitted |
| Citation | `cite` / linked reference | details on demand | full citation or resolvable short form |
| Cross-reference | `a` to stable ID | preview may be offered | page/section reference where available |
| Figure | `figure`, `figcaption` | responsive within measure | scaled without clipping |
| Table | semantic table elements | horizontal overflow only as last resort | repeat header; split rows only by policy |
| Definition | `dl` or defined term markup | hover/focus explanation optional | definition remains locatable in text/index |

## Interaction rules

- Interaction exposes context; it does not contain the only copy of substantive content.
- Hover behaviour must have equivalent focus, touch, and print treatments.
- Collapsed quotations show a meaningful lead and expansion control on screen; print expands them.
- Popovers do not trap focus, obscure their trigger, or require pointer precision.
- Internal references work as ordinary anchors without JavaScript.

## Export capability profiles

- `read-only`: semantic content, styles and minimal approved viewer functionality; remains natively printable.
- `read-pdf`: `read-only` plus an explicit native browser print/save-as-PDF interface.
- `editable`: `read-pdf` plus safely embedded canonical Markdown, text editing, local rendering and standalone HTML re-export.

All profiles preserve visible substantive HTML independently of JavaScript and share the same metadata and semantic vocabulary. Editing cannot depend on remote resources; the package contains no arbitrary author-executable components.

## Authoring directives

The Markdown adapter uses a small, versioned subset of MyST-style colon-fenced directives for components Markdown cannot express semantically. A provisional example:

```markdown
:::{sidenote}
:anchor: reasonableness
:label: Context

This test was reformulated in the 2024 amendment.
:::

:::{quotation}
:source: Act, s 12
:collapse-after: 8

Full quoted text…
:::
```

Directives are parsed into model nodes; their literal syntax is not part of the carrier format. Unknown directives are build errors.

## Conformance classes

- **Core document:** semantic HTML and CSS; no script required.
- **Enhanced document:** includes only versioned reference-reader behaviour.
- **Builder:** produces valid packaged documents from at least one source adapter.
- **Reader:** displays core documents and communicates unsupported profile versions.
- **PDF exporter:** meets the print contract and produces a fidelity report.

