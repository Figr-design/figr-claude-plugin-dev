---
name: wireframe-styling
description: Read before writing a Figr wireframe to /wireframes/<slug>.html over MCP.
---

# Wireframe Styling

## Delivery

A `data-wireframe` block is a file. `write_file` it to `/wireframes/<slug>.html` — the fragment only (no `<head>`, no wrapper document). The platform wraps it and serves it as a canvas node.

**Read before you edit.** `edit_file` matches the file's current text. If you don't already have those bytes this session, `read` first.

**Edits replace, they don't append.** "Add a section" means inserting sibling markup in the existing structure, not another wireframe after the closing tag.

`write_file` on an existing path replaces it — `overwrite: true`. `overwrite: false` errors instead of clobbering. New independent wireframe → new descriptive slug; prefer `edit_file` to change one you already wrote.

## Rendering format

Sandboxed iframe, scaled to the sidebar. Write HTML at full design width in `px` — the frontend shrinks it.

- Desktop — width 1280, viewport floor 800 — `data-wireframe="desktop"`
- Mobile — 390 × 844 — `data-wireframe="mobile"`
- Tablet — 820 × 1180 — `data-wireframe="tablet"`

```html
<div
  data-wireframe="desktop"
  data-width="1280"
  data-title="Settings — Account & Billing"
  data-bg="#ffffff"
>
  [content — no extra wrapper]
</div>
```

**Width is yours; height is not.** Do not set `data-height`.

**Applied at serve time (do not add):** title strip, outer border, body width, viewport-height floor, font-family, box-sizing reset.

**You must set:** `data-title` (short label) and `data-bg` (hex — always required).

## Color

Hex/rgb only. No `var(--*)`. Every `background`, `color`, and `border-color` is a hex/rgb value. Set background AND text together for contrast.

If a design system is attached, `read` it before the first frame. Grep `design.md` for surface/text/border roles, then `index.css` for the hex those roles resolve to. Take the values, not the token names.

## Fill the viewport

- Root → `display:flex;min-height:100vh`
- Every flex parent in the chain → `display:flex` + `flex:1`
- Main content → `flex:1`
- `vh` on the ROOT only

## Craft

Low in detail, not low in quality. Default to rough (boxes + zone labels). Move up only when they have engaged with the direction.

- Hierarchy before color. Density matches content weight.
- Product labels. Verb-led actions. No Lorem ipsum.
- One radius family. Softer greys (`#6b7280`) over harsh blacks.
- Inline styles only — no `<style>` blocks. No blank lines inside HTML (markdown splits on them).
- Sub-12px text — never. `position:absolute` for overlays only.

Then `figr build` is not required for a wireframe file; `finish_turn` still is after the write batch.
