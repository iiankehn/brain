# Slate release and data safety

## Release identity

| Item | Value |
|---|---|
| Package | `com.iiankehn.slate` |
| Version name | `YYYY.MM+<short commit>` |
| Version code | `1000000 + workflow run number` |
| Tag | `slate-YYYY-MM` |
| APK | `Slate-YYYY-MM.apk` plus `.sha256` |
| Update manifest | `slate-update.json`: `versionCode`, `versionName`, `apkUrl`, `sha256`, `sizeBytes` |
| Release notes | `docs/releases/YYYY-MM.md`, falling back to `RELEASE_NOTES.md` |

## Monthly workflow

`slate-monthly-release.yml` runs at 15:00 UTC on the 1st of each month, or by manual dispatch:

1. Derive version identifiers.
2. Restore the keystore from `SLATE_R1_KEYSTORE_BASE64`.
3. `gradle testDebugUnitTest lintDebug assembleRelease`.
4. Verify the APK signature, that the package is `com.iiankehn.slate`, the
   certificate against `SLATE_R1_CERT_SHA256` when set, and ARM64 plus x86_64
   coverage if there are native libraries.
5. Build the checksum and update manifest.
6. Create or refresh the GitHub release: a **draft** on schedule, published
   only by a manual dispatch with `publish: true`. Re-running in the same month
   moves the tag and replaces assets.

The `SLATE_R1_*` secret names are kept from Slate Notes, so the production
signing identity did not change when the products merged.

## Pre-release checklist

- CI tests, lint and release assembly pass.
- Existing Notes data upgrades without clearing app data.
- A previous signed build accepts the new APK as an in-place update.
- Note and Forge documents reopen after restart.
- `.slx` and `.slxf` exports round-trip.
- Oversized or malformed imports are rejected safely.
- Back navigation, keyboard insets, compact and expanded layouts are
  smoke-tested on hardware.
- The manifest URL, version code, size and SHA-256 match the APK.
- Release notes describe user-visible behavior and limitations.

## Rules that protect user data

- Never change the package, signing key or Notes database upgrade path without
  an explicit migration plan.
- Never publish a lower version code or a differently signed APK. Fix forward.
- Schema changes are additive, bump the version by one, and are mirrored in
  `documents` and `recovery_entries`. Never use a destructive fallback.
- Imports are untrusted and bounded. A failed import never replaces existing content.
- Never silently downgrade Forge content.

## In-app updates

**Check for updates** contacts the official GitHub release endpoint only when
the user taps it. Slate downloads the declared APK, verifies the size and
SHA-256, and hands it to Android's installer. Android verifies the signature,
and the update replaces the app without touching the library.
