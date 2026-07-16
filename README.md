# Figr - Claude Code marketplace (dev)

Dev/staging install source. MCP endpoint: **`https://dev-mcp.figr.design/mcp`**

**Live repo:** https://github.com/Figr-design/figr-claude-plugin-dev (public)

Prod counterpart: https://github.com/Figr-design/figr-claude-plugin → `https://mcp.figr.design/mcp`

## Install

```text
/plugin marketplace add Figr-design/figr-claude-plugin-dev
/plugin install figr-dev@figr-dev
```

Do **not** install both `figr@figr` and `figr-dev@figr-dev` in the same session if both register the MCP server name `figr` - pick one.

## Layout

```text
.claude-plugin/marketplace.json   # marketplace name: figr-dev
figr-dev/                         # plugin → install as figr-dev@figr-dev
  .claude-plugin/plugin.json
  .mcp.json                       # → https://dev-mcp.figr.design/mcp
  skills/figr-mcp/
```

## Sync from monorepo

Source of truth: `coding-agents/figr-claude-plugin-dev/` in private `figr-ai`. Push this folder’s contents to the public repo root when it changes.
