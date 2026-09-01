---
name: skill-creator
description: >-
  Org skill at /skills/{slug}/SKILL.md via Figr MCP. Read before creating or
  editing one, and when they state a standing rule without naming it.
---

# Skill Creator

An org skill is instruction text the org wrote for agents to follow. Packaged Figr
skills (this plugin) own product invariants; org skills own the org's taste,
defaults and process. Where both speak, take mechanics from the packaged skill
and judgment from the org skill.

Org skills are prose, not programs — write the rule in words. Nothing under
`/skills/` is executed. The mount is not listed at project root — `ls /skills/`.

## Steps

1. **Get the rule from them** — every line traces to something they said.
2. **Check for overlap** — `ls /skills/`.
3. **Pick the slug**, choose the mode, write the file.
4. **Verify** before reporting: `name` equals the folder slug, `mode` is `always`
   or `relevant`, body inside its cap, `relevant` has a non-empty description.
5. **Report** the mode and anything you wrote that they did not say.

## Get the rule from them

Do not invent a style guide they did not agree to. You need:

- The actual rules, specific enough to follow.
- When it applies, and where it stops.
- What they have been getting that they did not want.

Ask for what is missing as specific questions in one message. You are done asking
when every line you are about to write traces to something they said.

**Never invent:** a rule they did not state, and a scope wider than they asked for.

## Check for overlap

Read any org skill on the same subject. **Extend it** when the new rule applies
in the same situations. **New slug** when it applies in different situations.

## The file contract

New skill: `create_skill({ slug, content })`. Update: `write_file` or `edit_file`
on `/skills/{slug}/SKILL.md`. Copying an org skill folder is refused.

```markdown
---
name: brand-voice
description: Use when writing button labels, empty states, errors, or any UI copy.
mode: relevant
---

# Brand voice

Write labels as verbs the user is about to do — "Save changes", not "Submit".
```

- **`name` must equal the folder slug**, exactly.
- **Slug** is kebab-case (`a-z`, `0-9`, hyphens). Packaged slugs, `figr` and
  `conversation` are taken.
- **`mode`** is `always` or `relevant`.
- **`description`** ≤1000 characters; required when `mode: relevant`.
- **Body** ≤4000 characters for `always`, ≤10000 for `relevant`.

## Mode

**`always`** — whole body in every chat, org-wide. Tone, bans, defaults. Keep it
short. **`relevant`** — description is the retrieval key; default for scoped rules.

## Body

One rule per line, imperative. Say only what cannot be inferred. Show one example
where wording is the point. Leave dates out.

When the body outgrows its cap: keep `SKILL.md` as the decision layer and move
detail to `/skills/{slug}/examples.md`, linked from `SKILL.md`.
