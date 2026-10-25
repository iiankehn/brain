# Acute Web for iOS: architecture

A native SwiftUI application. WebKit provides rendering, networking, storage
and the sandboxed web-content processes. There are no third-party runtime dependencies.

## Structure

| Folder | Key types | Responsibility |
|---|---|---|
| `Model/` | `BrowserStore`, `BrowserTab`, `BrowserPreferences`, `BrowserSessionStore`, `SavedSiteStores`, `SitePrivacyStore`, `AddressResolver`, `WebAddress`, `ExternalLinkPolicy`, `BrowserChromeMode` | State, persistence, address parsing, policy |
| `Browser/` | `WebView`, `ContentBlocker`, `DownloadCenter`, `PermissionBroker`, `ScriptDialogBroker` | WebKit integration and brokers |
| `Views/` | `BrowserRootView`, `BrowserToolbar`, `NavigationTabCapsule`, `BrowserSidebar`, `StartPage`, `TabViews`, `SettingsView`, `SitePrivacyView`, `DownloadsView`, `TabletopControlDeck`, `AcuteGlass` | SwiftUI interface |
| `Commands/` | `BrowserCommands` | Menu-bar commands and keyboard shortcuts |
| Root | `AcuteWebApp.swift`, `PrivacyInfo.xcprivacy`, `Localizable.xcstrings` | App entry, privacy manifest, strings |

## State and privacy boundaries

- `BrowserStore` owns tab selection, session-only recent sites, closed-tab
  recovery and shared preferences. Each `BrowserTab` owns exactly one `WKWebView`.
- Regular tabs use WebKit's default data store. Private tabs share one
  non-persistent store, which is released when the last private tab closes.
- Tracker protection is a compiled `WKContentRuleList` evaluated inside WebKit,
  applied before main-frame navigation.
- `PermissionBroker` denies media capture until the user allows it once or
  always for a site. Prompts are cancelled when the tab closes, navigates or loses selection.
- `ScriptDialogBroker` presents website alerts, confirms and prompts natively, per tab.
- `BookmarkStore`, `HistoryStore` and `SitePrivacyStore` keep small Codable
  models in app preferences. History recording rejects private tabs before it reaches the store.

## Layout system

- `BrowserChromeMode` picks a compact capsule row, a wide row or a side rail
  from size classes and the system's vertical-bar edge, never the device model.
- `FoldLayout` turns iPhone Duo's fold regions into book or tabletop layouts.
- Regular-width windows use a split view with the Library sidebar.
- The navigation layer floats over WebKit content so Liquid Glass samples the
  page; measured scroll insets keep content reachable.

## Project and CI

- `project.yml` is the source of truth; XcodeGen generates `AcuteWeb.xcodeproj`.
  `MARKETING_VERSION` lives there, and CI sets the build number to the run number.
- The **Build** workflow on GitHub's `xcode-27` image (Xcode 27.1):

| Job | Runs |
|---|---|
| `simulator` (iPhone, iOS 27.0) | Validator tests, build-for-testing, unit tests twice with a simulator restart between, interface tests, privacy manifest validation, install and launch |
| `ipad-smoke` (iOS 27.0) | Layout interface tests, launch, keyboard/SwiftUI log checks |
| `iphone-duo` (iOS 27.1) | Unit tests and layout interface tests |
| `device-ipa` | Release build for arm64, `validate_release.py --release`, unsigned IPA, SHA256SUMS, `build.json` |
| `release` | Tag or manual run on `main` only: GitHub pre-release |

- Tests: about 20 unit test files in `AcuteWebTests`, plus `AcuteWebUITests`,
  `AcuteWebLayoutUITests` (portrait and landscape) and
  `AcuteWebAppearanceUITests` (accessibility audits in light and dark, largest text size).
- `scripts/validate_release.py` checks the built bundle: tracking disabled,
  empty tracking domains and collected-data arrays, exact required-reason APIs
  (UserDefaults CA92.1, FileTimestamp C617.1), and no debug fixture markers in Release.

## Constraints

- Swift cannot build on Linux, so cloud Claude sessions rely on CI.
- Only iOS 27 runtimes are available to Xcode 27.1, so iOS 18 to 26 are untested.
- No paid Apple Developer Program membership, so no TestFlight or App Store yet.
  `docs/BETA-READINESS.md` tracks App Review readiness separately.
