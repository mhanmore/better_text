# ADR 0001: Markdown canonical source with a Word style bridge

- Status: Proposed
- Date: 2026-11-10

## Context

The project needs a primary authoring representation that is reviewable, deterministic, and simple to transform, while remaining usable by professionals whose established drafting and review environment is Microsoft Word.

## Decision

Markdown (CommonMark/GFM plus a constrained MyST-compatible directive vocabulary) is the canonical source for the v0 reference workflow. In the optional editable HTML profile, this Markdown is safely embedded as the authoritative source; the rendered HTML is its derived view. The editor operates on Markdown text, not WYSIWYG HTML. Word documents using a published custom-style template are accepted through an importer that emits the same normalized document model. Word is not the canonical repository representation.

## Consequences

- Builders can generate repeatable output and useful text diffs.
- The semantic component set is explicit and testable.
- Word authors retain familiar drafting, tracked-change, and commenting workflows before acceptance into the build pipeline.
- The Word importer and its diagnostics become first-class deliverables.
- Arbitrary Word formatting will not be preserved; unsupported constructs must be reported.
- Exact Word round-tripping is out of scope for v0.

## Alternatives considered

### Word as canonical source

Strong author familiarity, but weaker diffs, merge behaviour, portability, and deterministic semantic extraction.

### Markdown only

Architecturally simple, but excludes too many target authors and review workflows.

### HTML as canonical authoring source

Closest to output, but too permissive and difficult to edit safely without a dedicated editor.

## Review trigger

Revisit after testing the Markdown and Word paths against at least three representative contract, legislation, or advice-note documents and collecting structured author feedback.

