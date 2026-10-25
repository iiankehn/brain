# CI lessons

Hard-won lessons. Read before debugging CI; add to this when something costs
more than one push to fix.

## Acute Web iOS (GitHub `xcode-27` image)

- A cold simulator runtime can spend about 10 minutes starting the test host
  before any test runs. Raise only the job `timeout-minutes`; never relax
  assertion timeouts or per-test waits.
- WebKit processes from an earlier test run can stall later website and
  download tests. CI restarts the simulator between the two unit passes and
  before the interface tests (#13, #14). Keep that when editing the workflow.
- `-collect-test-diagnostics never`: diagnostics collection once spent 10
  minutes timing out after failures. The result bundles still keep logs.
- Failed tests are not retried, and unit tests must pass twice. A "flaky" test is
  a real defect to harden (see #12), not something to retry.
- Xcode 27.1 cannot download iOS 18 to 26 simulator runtimes, so nothing below
  iOS 27 is tested. Do not re-add an iOS 18 job.
- iPhone Duo needs the iOS 27.1 runtime; iPhone and iPad use 27.0.
- Accessibility audits: contrast warnings that nearly pass are logged, not
  failed (#11). Duplicate keyboard shortcut registrations fail validation.

## Acute Web Android

- `make audit` runs locally in seconds and is the same gate CI runs first. Run
  it before every push.
- GitHub Actions must be pinned to 40-character commit SHAs; the audit fails otherwise.
- The Firefox commit is pinned in three places: `acute-android.toml`, the
  `PINNED_FIREFOX_REF` workflow env, and the manual-dispatch default. They
  must agree.
- Native startup crash fixed by isolating per-ABI APKs (`bf182a1`).

## Slate

- Emulator smoke tests were removed from CI in `c4fb57e`, after several commits
  trying to stabilize them. CI is unit tests + lint + assemble; layout and
  keyboard behavior need manual device smoke tests. Ask before re-adding emulator jobs.
