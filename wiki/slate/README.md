# Slate

**Slate by CORE** is a private, local-first Android writing app that adapts
from quick notes to full word-processing documents. In October 2026 it unified
the former Slate Notes and Slate Forge into one app.

| | |
|---|---|
| Repository | `iiankehn/slate-android` |
| Package | `com.iiankehn.slate` (inherited from Slate Notes so existing users upgrade in place) |
| Platform | Android 12+ (minSdk 31, targetSdk 36), ARM64 and x86_64 |
| Stack | Kotlin 2.3, Jetpack Compose (Material 3), Room 2.8, AGP 8.13 |
| Size | About 7,100 lines of app code, 1,600 lines of unit tests |
| Release line | Monthly, tag `slate-YYYY-MM`; current `slate-2026-10` |
| Distribution | Signed APK plus `slate-update.json` on GitHub Releases |

## Product promise

Open Slate and start writing. A document stays a lightweight **Note** until it
uses page-layout structure, then Slate keeps the complete **Forge** model,
without asking the user to pick an app first.

| Experience | For | Chosen when |
|---|---|---|
| Note | Notes, lists, journals, research, rich text | Default for adaptive documents |
| Forge | Letters, reports, manuscripts, page-structured documents | Explicitly selected, or required by structure |

Promotion to Forge is sticky. Length and word count never decide.

## Non-goals

- Two separately installed products
- Choosing Forge because a document is long
- Accounts or proprietary cloud services
- Claiming exact Microsoft Word layout parity
- Background update checks

## Pages

- [Features and formats](features.md)
- [Architecture](architecture.md)
- [Release and data safety](release-data-safety.md)
