# CORE Engineering Wiki

Reference for the products built under CORE: what they do, how they are built,
and how they ship. The Markdown here is the source; the same pages are
published to Notion ("CORE Engineering Wiki").

Facts come from each repository's code and docs as of 2026-10-25. Where a
repository's docs and its code disagree, the page says so.

| Page | Contents |
|---|---|
| [CORE overview](overview.md) | Portfolio, principles, how releases flow |
| [Acute Web](acute-web/README.md) | Product overview |
| [Acute Web features and parity](acute-web/features.md) | Feature sets on Android and iOS |
| [Acute Web for Android: architecture](acute-web/android-architecture.md) | Overlay build, channels, updater |
| [Acute Web for iOS: architecture](acute-web/ios-architecture.md) | SwiftUI/WebKit app structure, CI |
| [Acute Web: release, privacy and security](acute-web/release-privacy-security.md) | Signing, gates, privacy model |
| [Slate](slate/README.md) | Product overview |
| [Slate features and formats](slate/features.md) | Library, editing, formats |
| [Slate architecture](slate/architecture.md) | Layers, data model, persistence |
| [Slate release and data safety](slate/release-data-safety.md) | Monthly release, migrations, backup |
| [CORE website](core-website.md) | Publication, design system, publishing |
| [Engineering practices](engineering.md) | CI, conventions, Claude Code setup, known gaps |

Keep pages current: when a feature ships or a decision changes, update the page
in the same session (Claude: "update the wiki").
