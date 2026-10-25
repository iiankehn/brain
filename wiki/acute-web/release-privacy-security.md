# Acute Web: release, privacy and security

## Privacy model

| | Android | iOS |
|---|---|---|
| Telemetry, analytics, crash upload | Disabled by the overlay: product and marketing telemetry, crash reporting forced to Never, and diagnostic reporting | None present; privacy manifest declares no tracking or collected data |
| Browsing data | On device (history, bookmarks, passwords, downloads, tabs, Midnight preferences) | On device; history off by default; OS backups may include app data |
| Search | Selected provider | Selected provider (DuckDuckGo default); no suggestion requests while typing |
| Network calls by Acute itself | Update check to GitHub Releases | None |
| Sponsored or marketing content | Disabled (home content, onboarding) | None |

Websites, search providers and extensions have their own practices. Both
privacy policies say so.

## Android release pipeline

1. **Audit** (`make audit`): regression tests, JSON and XML parsing, app ID
   isolation, a non-exported update provider, HTTPS/GitHub-only updater, no
   debug or cleartext flags, no key material, SHA-pinned Actions, and agreement
   on the pinned Firefox commit.
2. **Metadata**: the tag selects channel, Gradle task and package; it must match
   `vX.Y.Z` or `vX.Y.Z-beta.N`.
3. **Unprivileged builds** per ABI, without release secrets.
4. **Isolated signing** in the `release-signing` environment (`ACUTE_KEYSTORE_B64`,
   `ACUTE_KEYSTORE_PASSWORD`, `ACUTE_KEY_ALIAS`, `ACUTE_KEY_PASSWORD`), plus a
   signer continuity check against v0.2.0.
5. **Publish** an immutable release with APKs, checksums, certificate and
   permission reports, build inputs and provenance attestation. Existing assets
   are never replaced.
6. **Website job** validates the release and updates `docs/index.html` via
   `scripts/update_site_release.py`.

Manual dispatch builds are debug-signed and never publish.

## iOS release pipeline

The Build workflow on a tag `vX.Y.Z` matching `MARKETING_VERSION`, or a manual
run on `main`, publishes a pre-release with `AcuteWeb-unsigned.ipa`,
`SHA256SUMS.txt` and `build.json`, after every simulator job and the IPA job
pass. Users sign with a free Apple account (Xcode, AltStore, Sideloadly); such
apps expire after 7 days and must be re-signed.

## Upstream security (Android)

The Mozilla commit changes only after reviewing security advisories, re-running
the overlay (fixing any fail-closed patch deliberately), a full build, package
and signature verification, functional checks, and an install over the
production release. An ESR-style cadence is preferred. Beta tests every pin change first.

## Signing keys

- **Android**: the release key is the permanent update identity. Keep two
  encrypted offline backups and record the certificate digest outside GitHub.
- **Slate** uses a separate key; see the Slate release page.
- **iOS**: CI does not sign.

## Reporting

Security issues follow each repository's `SECURITY.md`. Ordinary bugs go to GitHub Issues.
