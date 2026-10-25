# Acute Web

**Acute Web by CORE**, *the web, in focus*, is a privacy-focused browser with
two native implementations that share a product definition but no code.

| | Android | iOS and iPadOS |
|---|---|---|
| Repository | `iiankehn/acute-web-android` | `iiankehn/acute-web-ios` |
| Engine | Gecko (Firefox for Android, pinned commit) | WebKit |
| Language and UI | Upstream Kotlin + Acute overlay (Python patcher, resources, one Kotlin provider) | Swift, SwiftUI, about 5,800 lines |
| Identifiers | `com.acuteweb.browser`, Beta `com.acuteweb.browser.beta` | `com.acuteweb.browser.ios` |
| Minimum system | Android 8.0 | iOS 18 (only iOS 27 tested) |
| Distribution | Signed APKs (ARM64, x86_64) on GitHub Releases | Unsigned IPA on GitHub pre-releases; users sign and sideload |
| Channels | Stable (`main`) and Beta (`beta`), installable side by side | One pre-release line from `main` |
| Current version | Stable 1.1, Beta 2.0.0-beta.2 | 0.5 beta |
| Website | acute.iiankehn.com (from `docs/` in the Android repo) | Same site |
| License | MPL-2.0 (Mozilla-derived) | Repository license |

## Product definition

- A fast, standards-compliant browser with tabs, a unified search/address bar,
  bookmarks, history, downloads and private browsing.
- Nothing about browsing is sent to Acute or CORE. Search goes only to the
  provider the user picks (DuckDuckGo by default on iOS).
- Designed for phones, tablets, large screens and keyboard/pointer use from the start.
- Its own visual identity: Midnight interface and CORE Glass on Android, and
  Liquid Glass capsules on iOS. It should not look like a reskinned Firefox or Safari.

## Pages

- [Features and parity](features.md)
- [Android architecture](android-architecture.md)
- [iOS architecture](ios-architecture.md)
- [Release, privacy and security](release-privacy-security.md)
