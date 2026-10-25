# Playbook: bring a feature to the other Acute platform

1. Read `projects/acute-web.md` (parity table) and check the target platform is
   not feature-frozen (iOS: `docs/BETA-READINESS.md`).
2. Write the user outcome in one paragraph, independent of engine. Include the
   privacy implications and phone/tablet/large-screen behavior.
3. Map the implementation natively:
   - Android: an overlay patch in `scripts/apply_overlay.py` plus overlay assets,
     with fixture tests (`acute-overlay-patch` skill). Prefer upstream Gecko or
     Android Components behavior when it exists.
   - iOS: SwiftUI/WebKit in `AcuteWeb/`, unit tests in `AcuteWebTests`, layout
     and accessibility checks in `AcuteWebUITests`.
4. Match naming, settings labels and defaults across platforms unless a platform
   convention says otherwise.
5. Update the parity table once it ships.
