# brain

Shared memory for Claude Code across CORE projects. This should be a
**private** repository.

## How it works

1. Clone this repo next to your project repos (`../brain` from any project).
   In Claude Code cloud environments, add `iiankehn/brain` to the environment's
   repositories so it is cloned beside the others.
2. Each project's `CLAUDE.md` imports `@../brain/CORE.md`, so the short shared
   context loads automatically in every session.
3. Everything else here is read on demand when a task needs it.
4. Project-specific repeatable tasks are Claude Code skills inside each project
   (`.claude/skills/`). Cross-project procedures live in `playbooks/`.

## Layout

| Path | Loaded | Contents |
|---|---|---|
| `CORE.md` | Always (via import) | Portfolio, shared principles, how to work |
| `projects/` | On demand | Deep context per product, cross-platform parity |
| `playbooks/` | On demand | Multi-repo procedures (e.g. release → website → story) |
| `decisions/LOG.md` | On demand | Dated decisions and why |
| `learnings/` | On demand | CI and debugging lessons that cost time once |
| `inbox/IDEAS.md` | On demand | Unsorted ideas and follow-ups |

## Updating

Say "update the brain" at the end of a session. Claude records new decisions,
lessons and facts, then commits here. Review the diff like any other change.
