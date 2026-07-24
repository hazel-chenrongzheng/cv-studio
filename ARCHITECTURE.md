# Architecture

Everything is in `index.html`: `<style>` (CSS), the page skeleton (`<body>`), and
one `<script>` holding the data model, rendering, and export logic. There are no
dependencies and no build step — edit the file and refresh the browser.

## Data model

The whole app state is one `store` object, persisted to `localStorage` under the
key `cvStudio_v1`:

```js
store = {
  order:  ["r_ab12", ...],   // CV ids, in display order (the dropdown order)
  active: "r_ab12",          // id of the CV currently shown
  resumes: {
    "r_ab12": {
      label:   "EY 审计 SA1",   // name shown in the dropdown
      name:    "郑晨榕 Chenrong Zheng",
      contact: "phone | email | ...",
      sections: [ /* see below */ ]
    }
  }
}
```

A **section** is one of two types:

```js
// type "entries" — Education, Experience, Projects, etc.
{ title:"工作经历", type:"entries", items:[
    { l:"职位",  r:"日期",          // top line: bold title (left) + date (right)
      sub_l:"机构", sub_r:"地点",    // italic subline: org (left) + location (right)
      bullets:[ "…", "…" ] }
]}

// type "skills" — a list of "label: value" rows
{ title:"专业技能", type:"skills", rows:[
    { lab:"技能分类", val:"逗号分隔的技能" }
]}
```

If an entry's `sub_l` and `sub_r` are both empty, LaTeX export renders it as a
`\resumeProjectHeading` (title + date only) instead of a `\resumeSubheading`.

## Key functions (where to edit)

| Function | Purpose |
|---|---|
| `seedResume()` | The default CV loaded on first run. **Edit here to change starter content.** |
| `load()` / `save(now)` | Read/write `store` to `localStorage`. `save()` debounces; `save(true)` is immediate. |
| `active()` | Returns the currently selected résumé object. |
| `renderPicker()` | Rebuilds the dropdown from `store.order`. |
| `switchResume / newResume / dupResume / renameResume / delResume` | CV management actions. |
| `backup()` / `restore(input)` | Export/import the whole `store` as JSON. |
| `renderAll()` | Redraws header + body for the active CV. |
| `render()` | Builds every section, entry, bullet, and its ▲▼× controls. **Main view logic.** |
| `move(arr,i,dir)` | Swaps two array items (used by all ▲▼ buttons). |
| `mkBtn / mkEdit` | Helpers: a control button, and a `contenteditable` field bound to the model. |
| `esc(s)` | Escapes LaTeX special chars (`% & # _ $ \`). |
| `exportLatex()` | Rebuilds the `.tex` from the active CV. **Edit here to change the LaTeX template.** |

## Common changes

- **Change starter CV** → edit `seedResume()`. (Existing users keep their saved data;
  to force a re-seed, bump `LS_KEY` to `cvStudio_v2`.)
- **Restyle the résumé** → edit the CSS in `<style>` (`.name`, `.sec-title`, `.entry-*`,
  `ul.bullets`, print rules under `@media print`).
- **Change the LaTeX output** → edit the template string inside `exportLatex()`.
- **Add a new section type** → extend the `type` check in `render()` and in `exportLatex()`.
- **Add an English/Chinese toggle, drag-and-drop, backup reminders** → all live in the
  `<script>`; the data model already supports multiple independent résumés.

## Gotchas

- Data is per-browser (`localStorage`). Clearing site data wipes it — Backup guards against this.
- `contenteditable` stores plain text via `textContent`; no rich formatting is kept.
- LaTeX export assumes XeLaTeX + `ctex` for Chinese. For an English-only CV you can
  drop `\usepackage{ctex}` from the generated file.
