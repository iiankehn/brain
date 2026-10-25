# Inbox

Unsorted ideas, follow-ups and things to check. Move items to a project file or
the decision log once they settle.

- [ ] `acute-web-android/acute-android.toml` lists `release.candidate =
  "1.1.0-beta.1"` while Beta releases are at 2.0.0-beta.2. Confirm whether
  that field is still used or needs updating.
- [ ] `slate-android/CONTRIBUTING.md` says `./gradlew`, but there is no wrapper;
  CI uses Gradle 8.13 directly. Add a wrapper or fix the doc.
- [ ] iOS backlog after 0.5: Midnight-style dark pages and Read Aloud for parity with Android.
- [ ] coredotcom: `python3 tools/check_site.py --all` reports 47 legacy issues
  (as of 2026-10-25): 8 featured images not 1672 × 941, 11 cards missing
  `loading="lazy"`, and many card summaries reworded away from the article
  deck. Decide whether to fix them in one cleanup PR.
- [ ] Slate has no Room migration tests (`exportSchema = false`). Enable schema
  export and add `MigrationTestHelper` coverage before the next schema change
  (roadmap item 5).
