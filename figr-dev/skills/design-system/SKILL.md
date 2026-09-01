---
name: design-system
description: Read when creating, publishing, or consuming a Figr design system over MCP. Tokens-first, published package, figr publish.
---

# Design System (tokens-first)

Two modes. Don't mix the trees.

## Author

`create_design_system` or `set_design_system` — the session tree **is** the DS. Read `/SKILL.md` first.

Empty git. Figma import is optional. Write the package, then `figr publish` as its own shell command (not chained).

```
/
├── SKILL.md
├── index.css                — canonical tokens (Tailwind v4 `@theme` + `@utility`)
├── design.md
├── package.json             — name MUST stay `design-system`
├── src/index.ts             — public exports
└── src/components/<Name>/   — optional React components
```

Inside this package, import `"design-system"`. Prototypes consume the **published** name from the publish result (`figr-ds-…`), not these source files.

## Consume (project session)

A linked DS is listed at `/design-system/` — **read it, don't write it**. Never copy DS files into the app. Declare the published package in the app `package.json` and import that name.

**Do not write `/design-system/…` from a project session.** That creates a prototype folder, not DS git. Switch with `set_design_system`.

When `/design-system/…/agent/SKILL.md` or the DS `/SKILL.md` is present, it is the usage guide — don't bulk-read the rest.

If `package.json` `figr.template` is `ds-angular` (or `design.md` says Angular): `figr init <name> --template angular`.

## Tokens

A `@theme` token is already a utility — read its real name from `index.css` and write `bg-bg-muted`, never `bg-[var(--color-bg-muted)]`.

`ls` `uploads/` and `uploads/assets/` when the UI uses branding. Reuse those files before stock.

## Edit scope from a project

- **CAN:** `/<app>/src/` and the app `index.css` `@theme`.
- **CAN (user-requested DS work only):** `set_design_system`, then edit the DS tree, then `figr publish`.
- **Default:** don't edit the DS for routine prototype work. Missing token: app `@theme`. Shared DS change: author session, then `figr publish`.
