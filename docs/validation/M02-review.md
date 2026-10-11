# M02 independent acceptance review

**Date:** 23 September 2026. **Scope:** M02 only, against the real `Main`/`GameRoot` scene. M03 was not started by this review.

## Result

`tests/m02_smoke.gd` completed **49 checks with zero failures**, exit code 0, using Godot `4.7.2.stable.official.ed1daf0bf`. The final run's log is `builds/m02-tests.log`; it contains no engine warning, script error, or test failure.

```sh
"/Applications/Godot.app/Contents/MacOS/Godot" --headless --path . --script tests/m02_smoke.gd --log-file builds/m02-tests.log
```

Run the project's headless editor import first on a fresh checkout, so Godot registers the typed script classes. The final test was launched with normal macOS certificate/cache access. An earlier sandboxed launch passed its assertions but emitted a macOS certificate-access startup error; this did not recur in the final run.

## Verified behavior

- No distant target is selected at spawn. Area2D overlap detection finds both nearby fixtures; exact foot-position distance accepts 90 pixels and rejects 91 pixels.
- Authored priority outranks proximity, proximity outranks lexical stable ID, and an NPC entering range replaces an automatic doorway selection. Tab selects the doorway deliberately, wraps, and preserves explicit selection while it remains available.
- Unavailable targets cannot retain selection; activating with no target is harmless.
- E opens the correct authored text, input echoes cannot open or duplicate inspections, movement stays locked, and keyboard focus lands on Back. Return closes the focused Back button without reopening the world action; Escape closes inspection directly.
- All three fixtures can be inspected; repeated inspections do not duplicate IDs, and the objective visibly announces completion.
- P can pause an inspection. Reset cancellation preserves progress and the prior pause context; resuming restores the same inspection and Back focus. Focus-loss notifications pause an inspection and focus-return notifications never auto-resume it.
- At a 960 × 540 window setting, inspection text and Back remain in the viewport. A 36px, 24-line text fixture cannot overlap Back and has scrolling enabled for overflow.
- The marker toggle changes the controller and each actual target marker. Confirmed reset clears inspection IDs, target selection, modal state, and objective progress, restores spawn, and preserves marker preference.

The tie-order checks temporarily change fixture Resource fields in memory and restore them before the remaining checks. They do not edit source assets. This is an integration harness, not production gameplay code.

For a graphical screenshot of the long 36px inspection fixture, run the test without `--headless` and append `-- --capture`. That optional mode waits for a rendered frame, saves `builds/m02-inspection.png`, and adds one capture assertion. It intentionally skips capture when the display server is headless.

## Review boundaries

The runtime inspection confirmed that world interaction is routed through `_unhandled_input`, mode/pause ownership remains in `GameRoot`, reusable definitions are separate from room authoring, and marker visibility is applied to actual targets. No reproducible M02 defect was found in this review.

These checks do not establish native screen-reader support, every macOS window-manager behavior, or manual keyboard/mouse scrolling accessibility. Focus-loss checks dispatch Godot notifications directly. The root implementation task records the separate native graphical smoke check and M01 regression result.
