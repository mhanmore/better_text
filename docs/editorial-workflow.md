# Editorial Workflow

## Decision

Use Markdown as the canonical source for v0: CommonMark/GFM plus a small versioned MyST-compatible directive subset. MDX and author-supplied executable components are out of scope. Provide Word as a supported import environment through custom styles and a controlled conversion step.

This separates **authoring preference** from **document semantics**: authors may work in Word, but the repository stores normalized Markdown and/or the normalized model for review and repeatable builds.

## Markdown path

Recommended source layout:

```text
document/
  document.md
  metadata.yaml
  assets/
  references.yaml
```

CommonMark/GFM covers headings, paragraphs, emphasis, lists, links, quotations, code where permitted, tables within the chosen dialect, and images. Versioned directives cover provisions, call-outs, side notes, citations, definitions, and other approved components.

Full-editable HTML embeds the canonical Markdown as inert data, not as active script or editable rendered HTML. The optional CodeMirror editor modifies this Markdown and locally regenerates the semantic view; an export action produces a new complete `.html` file. The embedded Markdown and rendered document must be consistency-checked on export. The read-only and read + PDF modes may omit Markdown source.

Use MyST-style colon fences for Better Text-specific directives, for example:

```markdown
:::{sidenote}
:anchor: statutory-framework

The relevant test is fact-sensitive.
:::
```

The accepted directive names, arguments, nesting, escaping and syntax are specified by the Better Text profile: compatibility with all of MyST is neither assumed nor required.

The build reports source line numbers for invalid nesting, unresolved references, duplicate IDs, inaccessible labels, oversized assets, and print risks.

## Word style bridge

The Word template should expose a short style list and discourage direct formatting. Proposed styles:

| Word style | Normalized meaning |
| --- | --- |
| `Title`, `Subtitle` | document front matter |
| `Heading 1`–`Heading 4` | section hierarchy |
| `Normal` | paragraph |
| `Better Text Provision 1`–`Better Text Provision 4` | numbered provision levels |
| `Better Text Quotation` | long quotation |
| `Better Text Callout` | call-out block |
| `Better Text Side Note` | note anchored to the preceding marked text or paragraph |
| `Better Text Definition` | defined term and definition |
| `Better Text Citation` | citation record or citation-only paragraph |
| `Better Text Figure Caption` | caption associated with preceding figure |

Comments and tracked changes are editorial state, not carrier content. Import must refuse unresolved tracked changes by default and report comments rather than silently dropping them. Footnotes, endnotes, links, tables, and images use their native Word structures when they map cleanly.

## Why not Word as the canonical source

- semantic meaning can be obscured by direct formatting and theme changes;
- meaningful diffs and merges are difficult;
- deterministic builds require normalizing a complex package format;
- custom styles remain useful for contributors who prefer Word without coupling the carrier to one vendor.

## Why not Markdown alone

Many legal, policy, and business authors already rely on Word for review, comments, and tracked changes. A Word bridge is therefore a product requirement, not an afterthought. The bridge should be tested with real editorial documents before the v0.1 profile is declared stable.

## Round-trip policy

Lossless Word–Markdown–Word round-tripping is not a v0 goal. The supported direction is source import to normalized model to carrier. Exporting an editable Word copy may be offered later, with explicit diagnostics for structures that cannot round-trip.

