# Acute Web (Android + iOS)

One product, two native implementations. Shared principles, not shared code.
Tagline: *The web, in focus.*

## Side by side

| | Android (`acute-web-android`) | iOS (`acute-web-ios`) |
|---|---|---|
| Engine | Gecko, Firefox for Android pinned to one reviewed commit | WebKit (`WKWebView`) |
| Code model | Python overlay (`scripts/apply_overlay.py`) patches upstream Fenix in CI | SwiftUI app; `project.yml` → XcodeGen |
| IDs | `com.acuteweb.browser` / `.beta` | `com.acuteweb.browser.ios` |
| Channels | `main` = Stable, `beta` = Beta (separate app IDs, installable side by side) | `main` only; sideload pre-releases |
| Tags | `vX.Y.Z`, `vX.Y.Z-beta.N` | `vX.Y.Z` matching `MARKETING_VERSION` |
| Release | Tag push → audit → per-ABI build → isolated signing → GitHub Release → website job updates `docs/index.html` | Manual dispatch on `main` or tag → simulator jobs → unsigned arm64 IPA pre-release |
| Local checks | `make audit` (Python only) | `python3 -m unittest discover -s scripts -p 'test_*.py'` |
| Can build in cloud container | No (Gecko, CI only) | No (Xcode, CI only) |
| Product website | acute.iiankehn.com, served from `docs/` in the Android repo | Same site |
| Status (Oct 2026) | Stable 1.1, Beta 2.0.0-beta.2 | 0.5 beta, feature-frozen for release hardening |

## Shared behavior to keep consistent

- Zero telemetry, private browsing that never persists, search only to the chosen provider.
- Phone, tablet and large-screen layouts; keyboard shortcuts on large screens.
- Updates come only from the matching GitHub release channel.
- Branding: "Acute Web", "Acute Web by CORE". On Android avoid Firefox branding
  except accurate legal, license, source and engine disclosures.

## Parity

Parity is by user outcome, not by implementation. iOS beta scope is frozen
(see `acute-web-ios/docs/BETA-READINESS.md`): record Android features that
should come to iOS later in the backlog below, do not port them during the freeze.

| Feature | Android | iOS | Notes |
|---|---|---|---|
| Native x86_64 + ARM64 builds | Yes (1.1) | n/a | |
| Midnight / dark page treatment | Midnight Pages extension | Not yet | |
| Large-screen tab strip | Beta | Sidebar Library + optional tabs | |
| Read Aloud | Beta | Not yet | |
| Per-site privacy controls | Upstream Gecko site permissions | Site Settings list | |
| iPhone Duo / foldable layouts | n/a | Yes (0.5) | |

Update this table when a feature ships on either platform.
