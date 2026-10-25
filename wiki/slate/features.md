# Slate features and formats

## Library

| Capability | Behavior |
|---|---|
| Adaptive creation | New documents start without a Note/Forge decision; templates available |
| Classification | Note or Forge badge derived from persisted structure |
| Search | Title, body, folder and tags; saved searches per device |
| Organization | Pin, favorite, folder, tags, archive, trash, restore, duplicate |
| Version history | Preview and restore up to 30 local checkpoints per document |
| Recovery | Autosave after a short idle delay; startup recovers a newer checkpoint after an interrupted write |
| Encrypted backup | Whole library to a password-protected `.slatebackup` file |
| Restore | Preview, then keep both, replace existing, or keep newer |

## Editing

- Rich text: bold, italic, underline, headings, quotes, links, lists, checklists.
- Images and tables, with their own controls for descriptions and cell text.
- Find, undo and redo; shortcuts `Ctrl+B/I/U/F/Z/Y`.
- Forge structure: sections, page setup, margins, orientation, columns,
  headers, footers, page breaks, paginated layout.
- Notes use a continuous canvas without page chrome. Forge uses the paged workspace.
- Phones get a collapsible ribbon dock (bold, italic, underline plus More) and a
  compact landscape mode. Tablets get the expanded ribbon.
- Automatic light and dark appearance, including the canvas. This is display
  only: exports and prints use white pages.

## What promotes a document to Forge

Multiple sections, non-default page setup, headers or footers, non-continuous
section starts, structured tables, or forced page breaks. Nothing else, and
never length.

## Formats

| Format | Import | Export | Notes |
|---|---|---|---|
| `.slx` | Yes | Yes | Portable rich-note package; imports as Note |
| `.slxf` | Yes | Yes | Lossless Forge package: manifest, encoded model, checked assets; imports as Forge |
| TXT | Yes | Yes | UTF-8 |
| Markdown | Yes | Yes | Supported rich-text subset |
| DOCX | Yes | Yes | Practical interchange; advanced layout may simplify |
| PDF | No | Yes | Paginated output |
| Share and print | No | Yes | System share sheet (plain text) and print service (PDF) |
| `.slatebackup` | Restore | Backup | AES-GCM encrypted library container |

Conversions never modify the source. Forge to `.slx` creates a simplified copy.

## Platform behavior

- Phones, tablets, resizable windows and Googlebook Android environments, in portrait and landscape.
- System Back returns from a document to the library before exiting.
- Editor controls stay above the software keyboard.
- Screenshots and recent-app previews are blocked while Slate is visible.
- A user-triggered updater verifies size, SHA-256, package and signature.

## Known limitations

- The former standalone Forge app cannot hand over its database. Users export
  `.slxf` files and import them; a guided import assistant is on the roadmap.
- DOCX is interchange, not Word layout parity.

## Roadmap (from `docs/ROADMAP.md`)

1. Contextual Forge suggestions near page-layout actions
2. Guided import from the former standalone Forge package
3. Full accessibility audits (TalkBack, focus order, large text, contrast, keyboard, touch targets)
4. Performance benchmarks for large and image-heavy documents, pagination, startup, autosave
5. More migration, corrupt-package, fuzz, round-trip and updater security tests
6. Optional protected documents and encrypted exports
7. Later: templates, backlinks, attachments, quick capture, reminders
