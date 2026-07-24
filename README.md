# CV Studio

A single-file, offline-first résumé editor. Edit your CV visually in the browser,
manage multiple tailored versions, and export to **LaTeX** (Jake Gutierrez template)
or **PDF**. No build step, no server, no login — everything lives in one `index.html`.

Originally built to manage several role-tailored CVs (audit, business operations,
events, etc.) from one place, with full Chinese (CJK) support.

## Features

- **Inline editing** — click any text and type.
- **Reorder & delete** — hover any section, entry, bullet, or skill row for ▲ ▼ × controls.
- **Multiple CVs** — create, duplicate, rename, and switch between versions in one app.
- **Auto-save** — every edit is written to the browser's `localStorage`.
- **Backup / Restore** — export all CVs as one JSON file; import it on another browser or device.
- **Export LaTeX** — regenerates a `.tex` file (compile with XeLaTeX + `ctex`).
- **Print → PDF** — the toolbar and edit controls are hidden automatically when printing.

## Quick start

Just open `index.html` in any modern browser. That's the whole app.

To edit the code, open `index.html` in a text editor — all HTML, CSS, and JS are in that one file.

## Deploy (get a public URL)

**Netlify Drop (easiest):**
1. Go to https://app.netlify.com/drop
2. Drag `index.html` onto the page → you get a live URL instantly.
3. Sign up (free) to keep it permanent and rename the site.

**GitHub Pages:**
1. Push this repo to GitHub.
2. Repo → Settings → Pages → Source: deploy from `main` branch, root folder.
3. Your app is served at `https://<username>.github.io/<repo>/`.

## How your data is stored (important)

CV content is saved in the **browser's `localStorage`**, keyed to the site's URL.
It is **not** stored on any server or tied to an account.

- Closing the tab / quitting the browser / restarting the computer → **data is kept**.
- Clearing site data, or opening in a different browser/device → that browser starts fresh.
- Use **Backup** to download a JSON snapshot; **Restore** to load it elsewhere.

## Export → PDF via LaTeX

The **⬇ LaTeX** button downloads a `.tex` file. Compile it with **XeLaTeX**
(Chinese needs the `ctex` package). On [Overleaf](https://overleaf.com), create a
project, paste the `.tex`, and set the compiler to **XeLaTeX** in Menu → Settings.

## Project structure

```
index.html        The entire app (HTML + CSS + JS)
README.md         This file
ARCHITECTURE.md   How the code is organized — read before editing
CHANGELOG.md      Build history / version notes
LICENSE           MIT
```

## License

MIT — see [LICENSE](LICENSE). Résumé LaTeX template based on
[Jake Gutierrez's template](https://github.com/jakegut/resume) (also MIT).
