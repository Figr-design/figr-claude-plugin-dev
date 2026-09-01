---
name: prototype-constraints
description: Read before writing a Figr prototype over MCP. screens.figr.json, no fetch, figr init/build, VFS paths under /<app>/.
---

# Working in a Figr prototype

Write through MCP (`write_file`, `edit_file`, `shell`). Paths are `/<app>/…` from `ls` — never `/deepagent/…`.

**Yours vs ours.** `src/` is yours (`screens/` + the router shell). Never edit `figr-template.json`, `build.mjs`, or `tsconfig.json`. Don't rewrite the `package.json` `build` script.

**Scaffold + preview.** `figr init <app>` if the folder doesn't exist. After a write batch, `figr build <app>` — that stamps the canvas preview. Don't skip it. `publish_artifact` is a separate durable share URL.

**Screens index.** Maintain `src/screens.figr.json`. Multi-state UI: `?figr_screen=<id>` via `useScreenInit()` (React) or `screenInit()` (Angular).
- `screens` is an OBJECT keyed by screen id (`"scr_overview": { … }`), never an array. `sections`, `edges` and `layers` are top-level arrays — `edges`/`layers` never go inside a screen.
- Group by product area (`sections` + each screen's `section`).
- Different routes → different screens. Same route, different UI → same `route`, different `state`.
- Concrete paths only (`/users/42`), never `:id`. Don't write `position`. Leave `edges: []`.
- Update it when you add routes or meaningful states.

**Dependencies.** Anything the template didn't seed goes in `package.json` `dependencies` before you import it. List `@types/*` you never import under `devDependencies`. Never import a package you haven't declared. When consuming a design system, declare its **published** npm name (from `figr publish`, usually `figr-ds-<id>`) — not `"design-system"`. Don't hand-edit pinned versions.

**Sandbox.** The prototype has no Figr backend.
- No `fetch`, `axios`, or HTTP. Mock in component state; `setTimeout` for loading.
- No `localStorage` / `sessionStorage` — in-memory state only.
- No cross-app imports — each `/<app>/src/` is its own bundler. Share or fork with `cp`.

No `rm` / `mv` / `sed -i`. Chain shell with `&&`. Then `finish_turn`.
