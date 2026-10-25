# Engineering practices

## Repositories and CI

| Repository | Default branch | CI | Fast local check |
|---|---|---|---|
| `acute-web-android` | `main` (Stable); develop on `beta` | `validate.yml` (PR audit), `build-android.yml` (tags, `beta`, manual) | `make audit` |
| `acute-web-ios` | `main` | `build.yml` (push, PR, tags, manual) | `python3 -m unittest discover -s scripts -p 'test_*.py'` |
| `slate-android` | `main` | `android-ci.yml` (`main`, `beta`), `slate-monthly-release.yml` | `gradle --no-daemon testDebugUnitTest lintDebug assembleDebug` (needs the Android SDK) |
| `coredotcom` | `main` | GitHub Pages deploy | `python3 tools/check_site.py` |

GitHub Actions is the canonical build environment for every app.

## Conventions

- **Branches**: work on feature branches (`claude/...` for Claude sessions) and
  merge by pull request. Acute Android features go to `beta` first.
- **Commit messages**: Acute repositories and the websites use a plain
  imperative sentence ("Restart the simulator before the browser interface
  tests"). Slate uses Conventional Commits (`feat:`, `fix:`, `ci:`, `test:`, `release:`).
- **Pull requests** describe the user-visible outcome, risk, validation and
  limitations. Screenshots must contain no private content.
- **Never commit** keystores, credentials, APKs or IPAs, Mozilla source trees, or private documents.
- **Tests are never skipped or retried** to get CI green. Flaky tests are fixed at the root.

## CI lessons

- **iOS**: cold simulators can take about 10 minutes before tests start, so raise
  job timeouts, not assertion waits. Restart the simulator between test passes
  to clear WebKit processes, disable diagnostics collection, and remember that
  only iOS 27 runtimes are available.
- **Android (Acute)**: Actions must be pinned to full SHAs. The Firefox pin must
  match in three places. One ABI per build.
- **Slate**: emulator smoke tests were removed after repeated instability.

## Claude Code setup

| Layer | Location | Loaded |
|---|---|---|
| Shared context | `iiankehn/brain/CORE.md`, imported by each project's `CLAUDE.md` | Every session |
| Project memory | `CLAUDE.md` in each repository | Every session in that repository |
| Skills | `.claude/skills/` in each repository | When the task matches |
| Knowledge | `brain/projects`, `playbooks`, `learnings`, `decisions`, `wiki` | On demand |

| Skill | Repository | Use |
|---|---|---|
| `acute-overlay-patch` | acute-web-android | Add or change an upstream patch with tests |
| `acute-android-release` | acute-web-android | Beta or Stable release and website check |
| `acute-ios-ci-triage` | acute-web-ios | Diagnose a failing Build run |
| `acute-ios-release` | acute-web-ios | Version bump and pre-release |
| `slate-release` | slate-android | Monthly release notes and publish |
| `slate-db-migration` | slate-android | Safe Room schema changes |
| `core-story` | coredotcom | Research, write and publish stories |

## Known gaps

Docs and code that currently disagree, or missing safety nets:

- `acute-web-android/docs/TABLET_SUPPORT.md` says every build runs tablet launch
  and rotation smoke tests, but no workflow currently calls `scripts/tablet_smoke.sh`.
- `acute-android.toml` `release.candidate` is `1.1.0-beta.1`, while Beta is at 2.0.0-beta.2.
- `slate-android/CONTRIBUTING.md` uses `./gradlew`, but there is no wrapper.
- Slate has no Room migration tests.
- The CORE website has 47 legacy content issues (see the CORE website page).
