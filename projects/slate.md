# Slate (`slate-android`)

Private, local-first Android writing app. One app unifying Slate Notes and Slate
Forge since the October 2026 release (`slate-2026-10`).

## Identity that must not change

- Package `com.iiankehn.slate`, the existing production signing key (secrets
  `SLATE_R1_*`) and the Notes database. Notes users upgrade in place.
- Version name `YYYY.MM+COMMIT`, version code `1000000 + run number`, tag
  `slate-YYYY-MM`, asset `Slate-YYYY-MM.apk`, manifest `slate-update.json`.
- Never publish a lower version code or a differently signed APK. Fix forward.

## Product rules

- Note vs Forge is decided structurally (`DocumentExperiencePolicy`), never by
  length, word count or screen size. Forge never downgrades automatically.
- Imports are untrusted: keep size, path, entry-count and checksum limits.
- Only network path: user-triggered update check against GitHub.
- Formats: `.slx` (rich note), `.slxf` (lossless Forge); TXT, Markdown, DOCX
  import; PDF/print/share export.

## Engineering facts

- Kotlin + Compose, single activity, unidirectional state via `SlateViewModel`,
  Room persistence through `DocumentRepository`.
- Room schema version 4 (`data/SlateDatabase.kt`), `exportSchema = false`,
  hand-written `MIGRATION_n_m` objects.
- CI: `gradle --no-daemon testDebugUnitTest lintDebug assembleDebug` with Gradle
  8.13 and JDK 17. There is **no Gradle wrapper** in the repo, although
  CONTRIBUTING.md mentions `./gradlew`.
- Monthly release workflow runs on the 1st at 15:00 UTC and creates a **draft**;
  manual dispatch with `publish: true` publishes. Notes come from
  `docs/releases/YYYY-MM.md`, falling back to `RELEASE_NOTES.md`.

## Roadmap pointer

`docs/ROADMAP.md` in the repo is the source of truth for priorities.
