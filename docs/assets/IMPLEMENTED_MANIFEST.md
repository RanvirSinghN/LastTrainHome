# Implemented presentation manifest —25 September2026

This records the final vector/procedural implementation of the pre-production asset list. The original list estimated individual painted files. The implementation deliberately shares code and compositions instead of producing unused sprite sheets. These substitutions preserve story facts, readable interaction targets, five locations and three ending compositions. They are not claims that every originally estimated file exists.

| Planned group | Implemented source / deliberate substitution |
|---|---|
| BG01–05 | Five original SVG compositions in art/station,1920×720 platform and1280×720 interiors. Vector import replaces painted2× masters. |
| LY01–05 | Shelter,counter,bench,desk,cabinet forms in room SVGs. Foreground depth uses floor shadows and layered CharacterArt; no separate occluding sprites or navigation obstacles. Deliberately keep targets unobscured. |
| LY06–08 | Mountain/valley silhouettes in platform/carriage SVGs; original atmospheric fog gradient in StationAtmosphere. |
| PR01–17 | Clock faces,board,phone inspection UI,bench,timetable,map,vending,photo rack,visitor book,binder,deck,register,punch,supply,tray,service log in five compositions. Phone is a readable personal-phone transcript panel; no payphone. Targets retain discrete focus dots. |
| DR01–06 | Door/gate forms in SVGs; office-open inset in StationRoom. Door travel uses shared fade/open-close sounds rather than six frame animations. Upper gate departure uses platform composition and ending text. |
| TR01–03 | train_side.svg (body/windows/door), train doorway through staged text/fade, carriage_window.svg (empty seat/window). Door motion is deliberately implied rather than a second filmstrip. |
| OV01–08 | Runtime clock/board text,light strength,waiting-room rotated-chair overlay,office2026 notice,photo-facing state,scarf presence,relay indicators. No full room duplicates. |
| FX01–04 | Procedural rain lines,carriage condensation/rain lines,fog GradientTexture2D,radial light falloff. Reduced motion stops motion; reduced flicker replaces ripple with slow dimming. |
| World characters | Five articulated CharacterArt silhouettes,walking/breathing,distinct coat/hair/hat details. Replaces the planned28 drawn frames. No separate reaching sprite: interaction modal plus object sound conveys use. |
| Portraits |15 SVGs,three moods per character. Authored per dialogue node; neutral fallback. Ada appears only within the stylized historical photo. |
| Inventory | Six SVG icons plus explicit owned/installed/returned status. Punched ticket is described at Carriage commitment/epilogue and disabled in inventory; no ambiguous colour-only state. |
| Document groups | See mapping below. Text-first panels intentionally replace14 standalone painted close-ups. Text is enlarged/scrollable and stored in evidence/transcript; photo has its own image. No inaccessible text baked into textures. |
| Core UI | Existing title,pause,settings,reset,dialogue,inspection,inventory,notebook,map/transcript,puzzles,ending choices/confirmation/credits. Original flat frames and focus borders. Twelve planned action icons replaced with labelled controls and mapped-key hints; no new symbol vocabulary to learn. |
| Typography | Godot bundled fallback Noto Sans,display hierarchy through size/colour. Deliberately one readable family instead of two. Bundled font/engine notices extracted to CREDITS.txt. |
| Endings | Road dawn tint and extinguished board/train; Carriage still/window reflection/isolated weather; Witness restaged office,clock01:16,shared desk/record text. Existing locations reused. |
| Distribution | Original icon.svg and title wordmark in UI. Title reuses platform. Five native room screenshots available under builds/m14-*.png; final icon package/release captures audited atM16. |

## Twelve document groups

1. Return ticket front/back/date: H02,I01 description,M01 evidence; punched state in DG16.
2. Public timetable: H05 inspection,phase variants.
3. Station map: H06 and notebook Map.
4. Visitor book: H10 and C03.
5. Photograph front/reverse/caption: H09 image and DG11. Private reverse is not exposed without consent; credited caption retained in notebook.
6. Phone transcript: H03/C05.
7. Supply service card: supply puzzle panel,available beside controls.
8. Control slip: dispatch source panel/M02.
9. Dispatch/cue sheet: dispatch and cassette source panels,M03/I04.
10. Rescue appendix: DG09 andM05.
11.2026 handover/visitor list: DG09 andM06.
12. Service log/manual-record note: H17,DG12,C04.

Photo/ticket sides share a readable panel rather than separate image navigation. No extra puzzle information is hidden in an image.

## Sound routing

All49 source WAVs listed in audio_manifest.json. PCM imports are deliberate to avoid compressed playback issues; small game scope permits this. Dry masters excluded from export.

-7 beds: exterior/indoor wind,platform/window rain,fluorescent hum,heater beforeP2,distant rail bed onP1 platform. Later phases lower weather gain; heater stops atP2.
-9 footsteps: three variations per platform/tile/office wood.
-16 practical effects: travel open/close,successful office unlock,ending upper gate,paper inspection,Witness pen,DG06 cup/late waiting clock,vending beforeP2,cartridge/panel/reset/tape/playback mechanisms,Carriage ticket/door,ending-choice confirmation.
-6 textures: rail scrape at train reveal,stereo rail pass atP2 clock with caption,speaker click at wrong cue23 (also mixed into holding),tape hiss at unrecorded cues,carriage wheel loop,desk recorder signal.
-6 speech clips: first PA,CONTROL15,PLATFORM18,shared Road/Witness correction,Carriage next stop,blocked cue12. Witness uses a short derived V01 excerpt (no seventh source). Written words remain in required panels/transcript. Audition excerpt/mix with headphones and speakers duringM15.
-5 finite music cues: new journey,first cassette discovery,three ending commitments. No constant exploration music. Ending playback can be skipped with text advancement; no timed narrative dependency.

## Provenance / distribution boundary

Original project synthesis/vector code and system TTS; see PROVENANCE.md. Engine/font notices in CREDITS.txt. Public redistribution clearance for the system voice and signing/notarization remainM16 release conditions. Local evaluation is not advertised as a publicly cleared release.
