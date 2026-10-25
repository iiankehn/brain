# Playbook: ship a release across repos

Use this when an Acute Web or Slate release goes out. Each app repo's release
skill handles its own build; this covers what happens around it.

1. **App repo**: follow its release skill (`acute-android-release`,
   `acute-ios-release` or `slate-release`). Confirm the GitHub Release exists
   and its assets and checksums are correct before announcing anything.
2. **Product website** (Acute only): the Android release job updates
   `docs/index.html` automatically. Check the commit landed and the links point
   at the new release assets. iOS has no automatic site update.
3. **CORE Dev journal** (`core-dev`): add an article per its README. Use the real
   release date, link the release, list known issues honestly.
4. **Landing** (`landing`): update the project listing only when the headline
   version or feature set changes.
5. **CORE website** (`coredotcom`): only if a story is warranted; it is a news
   publication, not a changelog.
6. **Brain**: update `projects/<product>.md` status and the parity table, and
   log any decision in `decisions/LOG.md`.

Each repo is a separate branch and PR. Never claim device testing that did not happen.
