# Acute Web features and parity

Parity is about the user outcome. Each platform implements features with its
own engine and conventions.

## Shared feature set

| Area | Android | iOS and iPadOS |
|---|---|---|
| Tabs | Upstream tabs; persistent tab strip on large screens (Beta adds tab organization) | Capsule row of tabs; tab overview with previews, reorder, duplicate, reopen |
| Address and search | Unified search/address bar | Single capsule row with address, Back, conditional Forward, Refresh/Stop; local suggestions only |
| Private browsing | Upstream private mode | Non-persistent `WKWebsiteDataStore`; app-switcher shield; never in history or sessions |
| Bookmarks and history | Upstream | Folders, HTML import/export, start-page favorites; history off by default |
| Downloads | Upstream | Ask first, progress, resume, recovery after restart, search, preview, share |
| Find in page | Upstream | Live results, keyboard next/previous |
| Desktop site | Default on tablets; per-site overrides | Per-tab desktop/mobile switch |
| Page zoom | Upstream | Per tab, 50 to 200 percent, restored for regular tabs |
| Tracker protection | Gecko Enhanced Tracking Protection (upstream) | On-device `WKContentRuleList` |
| Per-site controls | Upstream site permissions | Tracker blocking, JavaScript, media capture, website data; Site Settings list |
| Updates | In-app check against the matching GitHub channel every 6 hours at most | Manual: download a newer IPA and re-sign |
| Keyboard shortcuts | Large-screen shortcuts (address, tabs, reload, history) | Full menu-bar commands: tabs 1 to 9, zoom, find, start page |

## Android-only

- Compatible browser extensions (Gecko add-ons).
- Midnight Pages (Beta): a bundled local extension that darkens sites without a
  suitable dark theme, with a per-site control.
- Read Aloud and tab organization (Beta).
- Picture-in-picture, split-screen and ChromeOS installation without a touchscreen.
- Saved passwords (upstream).
- Mouse back/forward buttons mapped to history.

## iOS-only

- Liquid Glass navigation on iOS 26+, with material fallbacks and Reduce Transparency support.
- iPad and iPhone Duo Library sidebar (Bookmarks, History, Downloads), with
  tabs optionally shown in the sidebar.
- iPhone Duo fold-aware layouts: book posture keeps controls clear of the fold,
  tabletop posture adds a control deck below it, and the outer display uses a side rail.
- Phone controls at the top or bottom, with optional automatic condensation.
- Confirmations before opening email, phone and message links in another app.
- Crash-safe restoration of regular tabs (can be turned off).

## Parity backlog

Candidates to bring to iOS after the 0.5 feature freeze:

- a Midnight Pages equivalent (dark rendering for sites without a dark theme);
- Read Aloud;
- tab organization (groups) on large screens.

Track decisions about these in the brain repository's `projects/acute-web.md`.
