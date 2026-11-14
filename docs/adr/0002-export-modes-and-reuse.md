# ADR 0002: Three portable export modes and reuse-first implementation

- Status: Proposed direction; dependency selection pending measured proof of concept
- Date: 2026-11-14

## Context

The original carrier-only architecture separates external authoring tools from finished HTML documents. Better Text can instead optionally carry a compact Markdown editor while retaining its readable-without-JavaScript semantic HTML and standalone offline operation.

Existing open-source components already address Markdown syntax, document directives and browser text editing. Rebuilding them before measuring their suitability would add unnecessary risk.

## Direction

Provide three standalone HTML capability profiles:

1. **Read-only:** semantic HTML, presentation and minimal viewer features; ordinary browser printing is still possible.
2. **Read + PDF:** read-only plus visible native browser print/save-as-PDF controls.
3. **Full editable:** read + PDF plus embedded canonical Markdown, plain-text editor, local parser and renderer, and HTML re-export as a new standalone file.

CommonMark/GFM is the source baseline. Specify a narrow MyST-compatible colon-fenced directive subset for Better Text semantics. MDX/JSX and executable author components are excluded.

Evaluate selected MyST packages for parsing, directives, document representation and transforms; evaluate CodeMirror 6 for the optional text editor. Neither is a fixed dependency until licences, tree-shaken browser size, security, compatibility and fidelity are tested. Do not bundle the full MyST publishing environment by default.

The single canonical source in an editable package is embedded Markdown; the rendered HTML is a generated snapshot. All export modes preserve complete semantic content without scripts.

Browser-native PDF is convenient but does not promise deterministic pagination across engines. Keep a separate pinned-browser build-time PDF exporter and parity tests for the reference output.

## Consequences

- The format remains readable, searchable and printable offline even with script disabled.
- The editable profile carries more JavaScript and requires clear content sanitisation and CSP checks.
- The editor is Markdown-first, not WYSIWYG.
- Save-as/download of newly generated HTML is the portable baseline; silent overwrite of the original file is not guaranteed, especially on iOS.
- A full-editor size target of roughly 750 KB–1 MB is provisional, not a measured result.
- Reader-only and read + PDF packages must not pay for the editing runtime.

## Validation before implementation commitment

Implement the proof-of-concept gates in [reuse-and-bundling](../reuse-and-bundling.md), including comparative bundle sizes, standalone `file://` use, iOS export, legal-document fixtures, offline safety and PDF fidelity.

## Alternatives rejected for now

- Building a new Markdown parser before benchmarking mature candidates.
- Using MDX/JSX as the document source grammar.
- A WYSIWYG editing surface.
- Bundling a general-purpose JavaScript PDF engine in every file.
- Assuming full MyST compatibility or adopting the entire MyST publishing stack.
