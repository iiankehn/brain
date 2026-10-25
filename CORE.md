# CORE shared context

Always-loaded essentials for every CORE project. Keep this file short: it costs
context in every session. Detail belongs in `projects/`, `playbooks/`,
`decisions/` and `learnings/`, which are read on demand.

## Owner and portfolio

Iian Kehn builds everything under the **CORE** brand. Focus projects:

| Project | Repo | What it is |
|---|---|---|
| CORE website | `iiankehn/coredotcom` | Static tech publication at core.iiankehn.com |
| Acute Web for Android | `iiankehn/acute-web-android` | Gecko browser: overlay on pinned Firefox for Android |
| Acute Web for iOS | `iiankehn/acute-web-ios` | Native SwiftUI + WebKit browser, sideload beta |
| Slate | `iiankehn/slate-android` | Local-first Kotlin/Compose writing app (Notes + Forge) |

Supporting sites: `core-dev` (dev.iiankehn.com, release journal), `landing`
(www.iiankehn.com, canonical shared Metro design). `core` is an unused EmDash
template import.

## Principles shared by every product

- Privacy first: no telemetry, analytics, ads, crash upload, accounts or
  background network calls. Any change to that is a product decision, not a code
  change: stop and ask.
- Distributed through signed GitHub Releases, not app stores. Never change a
  package ID, bundle ID or signing identity without an explicit migration plan.
- Fail closed: validators and patches stop the build rather than continue with
  unverified input.
- Honest claims: release notes, READMEs and articles never claim testing that
  did not happen (e.g. "passing CI is not device validation").
- Brand: **Acute Web by CORE**, **Slate by CORE**. Cat-fox mark across apps.
- Accessibility and phone + tablet + large-screen layouts are release
  requirements, not extras.
- Websites: plain HTML/CSS, no framework, no build step, dark-only Metro design.

## How to work

- Develop on a `claude/...` branch; never push to `main`/`beta` directly.
  Open a PR only when asked.
- CI on GitHub Actions is the canonical build for all three apps. Cloud
  containers cannot build Gecko or run Xcode; run the fast local checks the
  project CLAUDE.md lists and let CI do the rest.
- Commit style per repo: Acute repos use plain imperative sentences; Slate uses
  Conventional Commits (`feat:`, `fix:`, `ci:`, `release:`).
- Look in `projects/<name>.md` before planning cross-cutting work and in
  `learnings/` before debugging CI.

## Keeping the brain current

At the end of meaningful work, add what future sessions need: decisions to
`decisions/LOG.md`, hard-won debugging lessons to `learnings/`, new facts to
`projects/`, and loose ideas to `inbox/IDEAS.md`. Commit and push the brain repo.
Prefer editing an existing line over appending a duplicate. Never store secrets,
keystores, passwords or personal data here.
