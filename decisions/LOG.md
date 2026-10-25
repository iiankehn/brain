# Decision log

Newest first. One entry per decision: date, decision, why, where it applies.

## 2026-10-25 — Engineering wiki in Notion
The wiki's source is `brain/wiki/` (Markdown); Notion holds the readable copy,
kept private at the workspace level, outside the public-facing "CORE by Iian
Kehn" space. Why: searchable by Claude sessions and readable in Notion.

## 2026-10-25 — Shared brain for Claude Code
Shared context lives in a private `brain` repo imported by each project's
`CLAUDE.md`; repeatable per-project tasks are skills in each repo.
Why: one source of truth across repos without bloating every session.

## 2026-10-22 — iPhone Duo added to Acute iOS 0.5 scope
The device shipped October 23; support ships on simulator evidence plus tester
reports. Otherwise iOS beta scope stays frozen (no Android parity work).

## 2026-10 — Slate Notes and Forge unified
One package (`com.iiankehn.slate`), one database, one monthly release line.
Classification is structural; Forge is sticky.

## 2026-10-07 — Landing is the canonical shared web design
All CORE websites follow Landing's Metro layout, typography and tiles, with a
site-specific accent. Sites are dark-only.

## Standing — Acute Android channels
New features develop on `beta` and are promoted to `main` only after phone,
tablet, upgrade and update-channel testing. Upstream stays on a reviewed,
pinned Mozilla Stable commit.
