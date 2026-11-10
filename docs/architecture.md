# Architecture

## 1. Scope

Better Text is a **carrier format**, not an editor and not a new browser engine. An authoring tool compiles a supported source into one constrained HTML file. A normal browser is the primary reader. The browser's print engine produces PDF or paper from the same semantic tree.

The reference implementation should be usable as a command-line build tool first. Editors can integrate it later through the normalized document model and validation API.

## 2. Architectural principles

1. **Content before behaviour:** all substantive text is present in the HTML and visible without scripts.
2. **One semantic tree:** screen, print, accessibility, search, and PDF export share the same content and hierarchy.
3. **Closed package:** a conforming file performs no network requests and has no required external files.
4. **Small component surface:** every permitted component has explicit screen, print, fallback, and accessibility behaviour.
5. **Deterministic builds:** identical normalized input, template version, and build options produce byte-stable output where practical and visually stable PDF output.
6. **Validation at boundaries:** source import, normalized model, packaged HTML, and exported PDF are each checked.

## 3. Components

### Source adapters

- **Markdown adapter (normative for v0):** Markdown plus a small directive syntax for document-specific structures.
- **Word adapter (compatibility path):** `.docx` paragraphs and tables using approved custom styles. Direct formatting is treated as decoration, not semantics, and generates warnings when it cannot be represented safely.

### Normalized document model

A typed, ordered tree independent of Markdown and Word. Nodes carry stable IDs, semantic roles, numbering information, source locations, and optional provenance. This model is the point at which linting, cross-reference resolution, and policy checks occur.

### Renderer and packager

The renderer emits semantic HTML5. The packager embeds:

- the versioned screen and print CSS;
- the minimal approved reader script;
- compact fonts only when licensing and size policy permit;
- images as data URLs or embedded SVG;
- a JSON metadata block containing format version, build provenance, language, title, and integrity information.

The packager fails on external URLs in resource-bearing attributes unless they are ordinary user-followed hyperlinks and the chosen profile permits them.

### Reader behaviour

Reader JavaScript may add affordances such as collapsing a long quotation, opening an explanatory popover, copying a citation, or navigating cross-references. It must not fetch content, rewrite substantive text, or make any content inaccessible to print or no-script readers.

### PDF exporter

The reference exporter drives a pinned browser version with print backgrounds enabled, fixed page geometry, and an explicit print stylesheet. It records the browser/template versions in build metadata. PDF validation checks page size, embedded fonts, link targets, bookmarks where supported, and extracted-text parity.

## 4. File profile

The v0 carrier is a UTF-8 `.html` file. A dedicated compound extension may be adopted after interoperability testing. The root element declares a profile marker and version:

```html
<html lang="en" data-ohd-version="0.1">
```

The document includes a Content Security Policy meta tag that blocks network access and limits scripts and styles to embedded, build-generated content.

## 5. Safety model

The default profile prohibits:

- external scripts, styles, fonts, media, frames, and form submissions;
- arbitrary inline event handlers and author-provided executable code;
- service workers, local storage, cookies, analytics, and network APIs;
- automatic navigation or pop-ups.

Generated script should be hashable and versioned. A stricter `no-script` profile should remain possible. Opening a file must not itself contact the network; following an ordinary cited hyperlink is an explicit reader action.

## 6. Versioning and compatibility

- Format versions follow semantic versioning while pre-1.0 changes may be breaking.
- Each file declares its profile version.
- Readers ignore unknown non-substantive metadata but visibly flag unsupported semantic components.
- Builders can target an older profile and must fail rather than silently discard unsupported content.
- The specification repository contains frozen conformance fixtures for every released profile.

## 7. Repository direction

The likely implementation layout is:

```text
packages/model       normalized document types and validation
packages/markdown    Markdown adapter and directives
packages/docx        Word custom-style adapter
packages/render      HTML renderer and asset packager
packages/pdf         deterministic export and PDF checks
packages/cli         build, validate, inspect, and export commands
fixtures             source, HTML, PDF, and expected diagnostics
```

Language and dependency choices remain an implementation issue. A TypeScript implementation is a pragmatic initial candidate because the primary output and rendering environment are web-native, but the format itself must remain implementation-independent.

