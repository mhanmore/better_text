# Roadmap

## M0 — Decisions

- Confirm the Better Text profile identifier and file extension.
- Select licensing for code, specification, and example content.
- Approve the threat model and scripting policy.
- Approve CommonMark/GFM + constrained MyST-compatible directives, and the Word style map.
- Specify the read-only, read + PDF and full-editable export contracts.
- Benchmark MyST components and CodeMirror against a lightweight alternative (licences, size, offline operation, parser fidelity and security).
- Freeze the v0 semantic component palette.

## M1 — Executable specification

- Define metadata and conformance schemas.
- Integrate and adapt a tested Markdown parser and normalized document model; avoid rebuilding mature primitives without cause.
- Render a single self-contained HTML file.
- Implement the screen and print stylesheets.
- Add native browser print/PDF and a separate deterministic pinned-browser PDF export path.
- Create representative fixtures and automated fidelity checks.

## M2 — Portable editing and editorial bridge

- Add the optional CodeMirror-based Markdown editing layer in the full-editable profile, subject to dependency spike.
- Embed a single authoritative Markdown source and regenerate rendered HTML locally without network calls.
- Export a new standalone HTML file after edits; test browser file-saving limitations, particularly iOS.
- Verify source/rendered-content consistency and stable document identifiers across save/reopen.

- Publish the Word style template.
- Import `.docx` files that use the supported styles.
- Produce actionable import diagnostics for unsupported content.
- Add a document preview and validation report.

## M3 — Reader hardening

- Complete accessibility testing with keyboard and assistive technology.
- Add collapsible long quotations and non-disruptive detail panels.
- Add optional integrity metadata and signatures.
- Test major desktop browsers and offline transfer paths.
- Publish the v0.1 profile and reference implementation.

## Explicitly deferred

- General web application packaging
- Live collaboration or track changes in the output file
- DRM or access control
- Remote dependencies or analytics
- Arbitrary author-provided scripts
- Pixel-identical PDF output across unrelated browser engines
- WYSIWYG editing, general-purpose JSX/MDX execution, and arbitrary third-party directives
- Silent overwriting of the original local HTML file from every browser

