# Historical implementation journal — M04–M06

Entries record intermediate states, including failures subsequently fixed. GAME_STATE.md is the current handoff.

## M04 implementation journal

- Typed DialogueGraph/DialogueLine/DialogueChoice resources and DialogueController created, plus a nine-node fixture conversation with two tones, conditional callbacks, topic/exhausted replies and a required line. GameState records transcript and stable resume IDs. A separate NPC at x760 starts it. UI now supports full lines by default and a pause-menu typewriter preference. Import/tests pending; M04 remains incomplete.

- M04 graphical acceptance33/0 passed. Rendered minimum-size topic panel reviewed; placeholder portrait, focus and controls readable. Corrected a test-only KEY_RETURN typo to Godot KEY_ENTER. Earlier milestone regressions are running; M04.5 remains open until all exit cleanly.

- M04 COMPLETE:33 graphical checks and all prior regressions passed; see docs/validation/M04.md. DialogueGraph/Line/Choice and controller are implemented, including transcript/resume IDs and required-line reset. M05 now active; current usage30% used/70% remaining. No save service exists yet.

## M05 implementation journal

- Added ItemDefinition/ClueDefinition, InventoryController, six item definitions and separate evidence resource. Typed install/return effects validate OWNED before changing status. Added supplier dialogue, key cabinet and cartridge socket fixtures; inventory/notebook UI and I/J input now wired. DevelopmentCatalog centralizes explicit fixture paths. Import/tests pending; no acceptance claim.

- M05 first graphical route32/0 passed; evidence panel at36px/960x540 visually reviewed. Added inventory enlarged-text checks and unknown item-use-ID validation before final regressions. No known gameplay defect found; M05 gate pending those checks.

- M05 COMPLETE:final33 checks and all earlier regressions passed; see docs/validation/M05.md. Inventory/notebook and unique item ownership/status are implemented. M06 starting: safe disk snapshots, Continue, preferences and durable reset intent. Last usage50% used/50% remaining. No M06 code exists at this entry.

## M06 implementation journal

- SaveService autoload and strict version1 SnapshotValidator added. Writes are synchronous, rotate a validated backup, publish via temp rename, and reject stale generation tokens. Reset intent persists before clearing only run files; preferences remain separate. Tests M01–M05 now set isolated build-directory storage before creating Main, protecting user saves. GameRoot save/Continue wiring and M06 tests still pending; checkpoint incomplete.

- M06 integration wired: title Continue, confirmation for New journey over an existing save, safe-boundary/coalesced autosaves and2-second exploration position snapshots, modal/required-line resume, persisted marker/typewriter preferences, coordinated full reset and boot recovery. UI warns on save/reset failure; all test storage remains under builds/test_saves. Import and acceptance still pending.

- M06 import clean. First M05 regression exposed an outdated assertion: autosave now legitimately records the new player position during a refused item use. Updated that test to compare all state except player_x; item/flag/evidence invariants remain checked. Dedicated save/reset matrix still pending. Usage64% used/36% remaining.

- M06 first dedicated matrix found a genuine disk-reload bug: JSON numeric values made strict nested puzzle-default Dictionary equality fail. Replaced it with per-field type/value checks and canonical integer normalization. Earlier assertions failed downstream of this cause; the final matrix is being rerun. M06 NOT complete.

- M06 dedicated matrix38/0 now passes; JSON numeric normalization fixed. Malformed-JSON fallback initially printed parser errors despite recovering; switched to JSON.parse with explicit error return for clean expected failure handling. Added an always-visible persistence notice so save/quit errors are not hidden behind modals. Cross-process persistence and full regressions are pending. Usage75% used/25% remaining.

- M06 COMPLETE:220 checks across all six suites, plus4 separate-process persistence checks, all clean. See docs/validation/M06.md. SaveService now exists; older journal notes saying otherwise describe prior stages. Current schema is version1 (single fixture room/phase0); extend it before saving additional rooms/phases in M07. M07.1 next; no room/audio code yet. Last usage75% used/25% remaining.

### M07 intermediate — room travel
RoomDefinition/RoomCatalog, explicit doors and phase fixture implemented. Root owns a pauseable 0.6s fade; room replacement happens at black. Recovery policy: save source until swap, destination after swap, normalize fade to PLAYING on load. Same v1 shape remains backward compatible; validator expands its trusted room/entry/phase vocabulary. Initial M02–M05 regressions pass. M06 exposed JSON numeric membership mismatch (float phase versus integer array); changed validation to numeric comparison. M07 is not passed; audio and dedicated integration test remain.

### M07 intermediate — audio and integration
AudioDirector is now the third autoload: Master/Ambience/Effects/PA/Music buses, temporary generated WAV tones, two-bed crossfade, one PA player. StoryDirector retains durable cue ownership and stable priority; captions are required inspection modals and acknowledge explicitly. Pause suspends playback and fade timing; reset cancels both. Dedicated M07 test: 26 checks pass. Mixer shutdown needed 0.2s after stopping streams in the test (otherwise pending audio cleanup produced ObjectDB warnings). Existing M01–M06: 220 checks passed before audio integration; final regression pending. Usage check: 29% used, 71% remaining.

### M08 intermediate — shared puzzle system
Added PuzzleRules, PuzzleController and three typed puzzle scene instances using a shared panel. State service owns partial edits, installation and atomic solved rewards. Version2 writes retain v1 read support; old cassette records receive false kept-excerpt fields. Puzzle modal context restores through Continue. Added annex puzzle targets, a conditional archive-technician conversation for I05, required first PA and labelled witness-completion fixture. Editor import passes. Dedicated playable-route tests and rendered layout review still required; M08 is NOT passed.

### M08 intermediate — playable route verified
39 dedicated checks pass headless and in a native macOS window. Reviewed screenshots of all three panels; controls and Back are visible, source/transcript areas scroll. Fixed incorrect overlay property access. The first native route ran before macOS focus settled; test now waits 0.8s before starting and explicitly resumes an external focus pause during scripted navigation. Production focus-loss pause behavior remains unchanged. Full regression is running. Latest usage check: 48% used, 52% remaining.

### M09 intermediate — ending and checkpoint implementation
Added EndingDefinition/Catalog/Director/Panel and playable engineering fixtures for mandatory witness record, optional C02/C04, consent and repair conversations, plus three shared decision hotspots. GameRoot modes END_CHOICE/END_CONFIRM/ENDING; two-step confirmation preserves I01 until Carriage commit. Save writer v3 reads v1/v2 and adds ending_beat default. Checkpoint is validated/written at eligible panel entry and immediately before commit; ending saves do not overwrite it. Revisit copies it into the active run. Import passes; M09 tests not yet run, gate remains open.

### M09 complete — final handoff
All395 milestone assertions pass; native M09 passes102. Fixed typed array concatenation in DevelopmentCatalog (append_array preserves Array[StoryAction]), added scrolling to long relationship choices, and verified checkpoint failure blocks commitment. Repair sets, evidence notebook entries, v3 migration, staging/credits resume and post-credit reset are complete. Captures reviewed. M10 is next and NOT started. Latest usage90% used /10% remaining; stopped at a verified gate to preserve a clean handoff before allowance expires. No reset credit consumed.

Final native launch found forced --quit-after bypassed audio cleanup. Added normal Quit mixer drain (0.2s) and duplicate-quit guard; tests/quit_smoke.gd runs actual main scene, starts a fresh isolated run and invokes menu Quit. Native normal shutdown is clean. Forced engine termination can still bypass graceful cleanup, as expected.

Final allowance check:99% used,1% remaining. Clean handoff saved; M01–M09 complete, M10 not started.

### M10 intermediate — authored opening implemented,24 September
Default Main now selects production; fixture_main preserves M01–M09 route for tests. Five separate station scenes use a clean shared station shell, not fixture targets. StationRooms owns exact graph/positions/inspection variants; DG01–DG06, actions/items/clues are typed .tres authored by tools/author_opening.py. Production saves use user://station (legacy fixture saves preserved). Ivo-first/skipped-board and Mira-first/lie routes both pass;43 M10 checks cover P0 key/office access, repairable Leon technical explanation, supply/P1, first PA/DG06, S04 endpoint, changed props, Continue and reset. M10 remains open pending native layout review and full regression. Later content is explicitly bounded, not silently missing.

### M11 active — mandatory continuation
Authored DG07–DG09, DG14/DG15 and M02–M06 with exact chronology. Added Ivo cassette handover on either tone, rescue/current-date acknowledgement actions, D05, P3 platform trigger, late NPC staging, stationary train and seven-beat Road sequence with Ivo/Mira/scarf variants. Production Carriage/Witness remain explicitly not-authored until M12. S04 endpoint removed from progression; legacy BUILD_END saves resume exploration. Fixed an indentation error in changed binder inspection. M11 import recheck/test route pending; do not advance.

### M11 intermediate validation
Both complete authored Road routes pass48 checks headless/native. Tests play all puzzles and both Ivo tones with a lie to Mira, requested distance and no optional clues. Mandatory dates/rescue/no-causal-overclaim text, witness resume, NPC relocation, platform scene, all Road beats, credits and revisit pass. Corrected late clock/timetable inspection text and Mira's late response. Other endings explicitly show coming in M12, not permanent story locks. Full regression running. Usage69% used /31% remaining.

### M11 accepted; M12 begins
All490 checks pass, including48 authored Road checks headless/native. Final hint and Road presentation corrections pass targeted rerun. M12 starts with optional investigation; no M13 work authorized before its gate. Usage79% used/21% remaining.

## M12 intermediate —optional investigation implemented, validation pending
DG10–DG13 now cover scarf memory/return, Tess’s separate public-use consent/refusal/repair, Mira’s trust repair, Leon’s C04 manual-recording explanation and Ivo’s present-day questions. Dynamic optional graph routing is in StationRooms.optional_dialogue and GameRoot; scarf use opens a conversation before an explicit return choice. Notebook appends discovered scarf memory and consented caption. StoryRules adds validated trust_below for repair visibility. tests/m12_optional_smoke.gd plays the actual late route to all11 clues and both repairs; not yet passed. Remaining: fullDG16/DG17 ending scenes, late-response audit, six principal authored routes and M12 gate. Do not mark M12 complete.

### M12 optional slice validated; allowance handoff
33 native optional-route checks pass and48 Road regression checks pass. All11 clues, scarf return, separate photo consent, both repairs and Continue verified. No M12 gate claimed. Remaining full endings/branch matrix listed in GAME_STATE.md. Stopping new feature work at96% five-hour usage; no reset credit used.

### Art direction update —24 September2026
User requests more colourful artwork and denser environmental props, including non-interactable decoration. In M13/M14 use varied muted jewel colours (teal, moss, ochre, rust, warm amber and cooler mountain blues), localized warm light and readable silhouettes rather than a uniformly grey station. Dress rooms with luggage, cups, posters, plants, shelving, tools, cable runs and weathered railway fixtures. Decorative props must not inflate the24-hotspot scope, obstruct navigation or masquerade as mandatory interaction prompts. Keep the melancholy/eerie tone through lighting, sound and subtle changes, not blanket desaturation.

### Eerie simulated lighting —user requirement,24 September2026
M13/M14 animation work includes layered simulated lighting: warm amber lamps against cold blue/teal platform spill, soft shadow movement from weather outside, gentle lamp falloff, occasional localized fluorescent dips and slow phase-driven changes. Use Godot2D light/shadow layers or equivalent authored overlays, keeping colourful materials visible. No rapid flashes or abrupt full-screen blackout; reduced flicker defaults on and replaces flicker with slow dimming, while reduced motion freezes moving shadows/parallax. Required objects, text and walk paths remain readable. Verify normal/reduced settings in native captures and phase revisits.

### M12 accepted; M13 starts
All623 assertions pass across completed milestones. Full endings and replay now live; gate evidence docs/validation/M12.md. Art direction: colourful dense room dressing and eerie simulated lighting, reduced-motion/flicker-aware. Planning workflow points6–10 integrated, REVIEW.md created. M13 begins with reusable opening presentation/settings.

### M13 intermediate
Authored two colourful SVG room compositions with decorative props and reusable simulated lighting/weather. Added settings panel and validated preference schema, preserving existing settings on reset. Key conflicts are refused; Escape remains fixed for menus. M13 not accepted; import and layout tests next, then character animation/portraits and sound treatment.

### M13 native review and regression fixes
Native settings11 checks pass. Screenshots confirm coloured room dressing, local lighting and Rowan/Mira portraits. Fixed typed Array assignment in lighting draw and wrapped HBox puzzle-button collapse; final puzzle suite41 passes. Other impacted suites pass. M13 remains open for sound and full presentation/accessibility audit. Stopping new feature work at92% usage; exact handoff saved.

Final handoff verification: builds/m13-settings-final.log passes11 native checks; builds/m13-all-endings.log passes70 checks across all six authored routes after presentation changes. Both processes exit0 with no reported runtime errors/warnings. M13 remains in progress; no M14 work begun.

### M13 continuation —fresh allowance window
Added original synthesized wind/rain/hum/footsteps and a processed holding announcement (macOS Samantha system TTS, original text, dry AIFF retained). Production audio replaces test tones; fixtures retain their tone bed. Added permanent PA transcript, explicit portrait states, all menu/footer control hints, and reduced-motion inheritance on NPC restaging/camera. Native size/fullscreen/complete-route acceptance is next. M13 remains open until validation passes.

### M13 accepted
All656 assertions pass. Native minimum-size/text/fullscreen plus opening-to-Road verified. Complete opening audio, permanent PA transcript, emotion-state selection, dynamic control hints and restaging preferences integrated. M14 begins; usage35%.

### M14 presentation integration — in progress
Five backgrounds,15 portraits,six icons,train side/carriage/photo authored.49 audio source slots generated; system speech sandbox initially returned empty files despite zero exit. Added minimum-duration assertion and reran with system speech access. First branch regression70 assertions passed but engine audio errors invalidate acceptance. Imports pinned to PCM; native audio/room acceptance added. Remaining: clean checks, asset/routing reconciliation, credits/provenance and export smoke.

Speech regeneration with system access produced49 nonempty PCM sources; all six spoken clips contain data. Caption wording aligned with cassette text. Fixed visible physical-key suffixes, carriage markers/player appearing over window composition, and overly dark ending overlay. Native64 and six-route70 reruns in progress.

M14 final session handoff: native64,branches70,accessibility22 clean. Export succeeded; native packaged180-frame launch exited0, with4 ObjectDB leak warning on forced shutdown (normal exported Quit pending). Docs synchronized including exact remaining M14 scope. Usage91%; no acceptance claim/M15 advance.

### 25 September — fullscreen report
Native fullscreen entered externally was being overridden by saved false during room preference application. Apply window mode only at startup or explicit preference change; settings reads actual mode. Native tests/m14_fullscreen.gd10/10 pass. M14 presentation polish continues; no M15 advance yet.

M14 accepted25 September:718 sequential regression assertions; expanded native70/final routes70/fullscreen10 clean. Export regenerated with gate detail,opened via macOS and Quit through UI clean. M15 now starts; no M16 work before human QA gate.

M15 technical QA36 restart +69 native checks passed. True-zero mute/early-clock wording fixed. Human playtest form ready; user asked, no observations received. Usage96%; handoff saved. Refresh export for last2 source fixes next; no M16 advance.

##27 September2026 — M16 packaging active
User deferred human testing until after M16. Production now instantiates its own initial room; fixture factories/scenes/data excluded from export with lth_release feature. App renamed Last Train Home, version1.0.0-rc1; explicit custom user path preserves existing Development saves. Icon generated from original SVG. Full regression underway; one transient fixture shutdown warning did not reproduce in verbose isolated run. Apple System Voice SLA audit confirms public redistribution blocker; local personal candidate remains target. Usage34% at latest check.

##27 September2026 — M16 local candidate accepted
Full source regression724 clean after removing obsolete endpoint assertion. Final PCK checks117,package audit14,nativefullscreen10 pass. PCK harnesses must run outside sourcecwd; otherwiseResourceLoader can fall back to files intentionally excluded from export. Stockrelease executable disables --script; use matchingengine with --main-pack for automation and exactapp fornativeUI smoke. Exactapp launch/settings/normalQuit clean. Originalicon/version/bundle finalized; existinguserpath preserved. ZIP sealed in tempstorage to avoid cloud-addedFinderInfo; ad-hocsignature verified. SHA and sources in builds/release/BUILD_MANIFEST.json. HumanM15 deferred by user, publicvoice/signing/Intel limits documented. Allmain planning/state/review/bible/testing docs updated. No public release claim.

Final handoff usage83% consumed /17% remaining. Final ZIP CRC/hash/signature and byte-for-byte identity with native-tested app verified. No game test process left running. User human testing is next.

##27 September2026 — public written-dialogue edition
Removed every production load of the six Samantha recordings and the derived Witness fragment. The opening PA now uses a speaker click; cassette PLAY uses tape hiss/click while showing the full excerpt; ending statements remain written dialogue with music/effects. Updated all three credit screens and CREDITS.txt. Public export excludes `audio/voice/*`. Exported version1.0.0, strictly verified its ad-hoc signature, scanned the PCK/export log for voice paths and launched/quit the exact archived app cleanly. Public ZIP and hash recorded in docs/validation/PUBLIC_RELEASE.md. Historical RC1 remains private and must not be uploaded.
