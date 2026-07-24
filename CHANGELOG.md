# Build history

The "thread" of how this app came together, newest first. Useful as a record of
decisions and as a map of what to build next.

## v1.0 — CV Studio (multi-version app)
- Refactored into a résumé **manager**: multiple CVs held in one `store`, with
  create / duplicate / rename / delete and a dropdown to switch.
- Moved `name` and `contact` into each résumé's data (were previously hard-coded),
  so every version is fully independent.
- Added **auto-save** to `localStorage` (debounced) with a "Saved ✓" indicator.
- Added **Backup / Restore** (JSON export/import) for moving between devices,
  since `localStorage` is per-browser.
- Filenames for LaTeX export now derive from the CV label.
- Saved as `index.html` for one-drag Netlify / GitHub Pages deploy.

## v0.3 — Reordering
- Added ▲ ▼ move controls (plus × delete) to **sections, entries, bullets, and
  skill rows** via a generic `move(arr, i, dir)` helper.
- Controls hidden in print output.

## v0.2 — Editor with export
- Made the whole résumé editable inline via `contenteditable`, bound to a JS data model.
- Add/remove for entries, bullets, and skill rows.
- **Export LaTeX** — regenerates a `.tex` using the Jake Gutierrez template.
- **Print → PDF** with a print stylesheet hiding the UI chrome.
- **Save HTML** to keep a static copy.

## v0.1 — Static LaTeX résumé
- Tailored an EY Audit (French group) SA1 résumé from past CVs.
- Chinese LaTeX résumé using the Jake Gutierrez template + `ctex`, compiled with XeLaTeX.
- Verified one-page layout; no summary section.

## Ideas / backlog
- English ⇄ Chinese toggle per résumé.
- Drag-and-drop reordering (in addition to arrows).
- "You haven't backed up in N days" reminder.
- Optional cloud sync (e.g., GitHub Gist or a small backend) to replace manual Backup/Restore.
- Direct PDF export (client-side) instead of the print dialog.
