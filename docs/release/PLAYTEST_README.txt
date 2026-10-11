LAST TRAIN HOME — 1.0.0-rc1
Personal local macOS playtest • 27 September 2026

PLAY
Extract the ZIP into a local folder such as Downloads and open Last Train Home.app.
No Godot installation is needed. This is an ad-hoc signed local candidate, not an
Apple Developer ID signed/notarized public release. Only Apple M4 on macOS 26.6.2
has been tested. The executable also contains Intel code, but Intel is untested.

CONTROLS
A/D or arrows: walk. Shift: faster walk. E: inspect/talk. Tab: cycle nearby targets.
I: inventory. J: notebook. P/Escape: pause. Mouse and keyboard operate menus.
Settings offer text sizes, remapping, fullscreen, volumes, reduced motion and
reduced flicker (on by default). Losing focus pauses the game.

SAVES
Continue resumes your autosave. Revisit the decision restores the earned
pre-ending checkpoint. Reset Game asks for confirmation, clears the journey,
autosave, backup and ending checkpoint, then starts fresh. Settings are retained.
The app intentionally uses the old save directory to preserve existing progress:
~/Library/Application Support/Godot/app_userdata/Last Train Home — Development/station
New journey also asks before replacing an existing journey. Tests used isolated
save folders and did not reset your personal progress.

TESTING
All three endings and optional investigation are implemented. Play naturally;
record active play time, puzzle difficulty, confusing dialogue, unreadable text,
sound issues and the ending you reached. The 28–35-minute target has not yet been
measured by first-time human players. Human pacing/listening tests are your next
step; automated route timing is not a substitute.

LOCAL USE ONLY
Six speech recordings use Apple's Samantha system voice; the Witness texture
also contains derived speech. macOS Tahoe Software License Agreement section 2F
restricts System Voices to personal non-commercial projects and prohibits public
sharing/redistribution. These recordings must be replaced before public release:
https://www.apple.com/legal/sla/docs/macOSTahoe.pdf
Original scripts, art and synthesized non-speech sounds remain usable project
assets. Godot and third-party notices are included in CREDITS.txt.

TECHNICAL NOTES
Godot 4.7.2 Standard, Compatibility renderer. Engineering fixtures, tests, tools,
design documents and dry voice masters are excluded from the game pack.
No known reproducible progression/save/reset blocker remains in the tested routes.
Other Macs/OS versions, extended performance, laptop-speaker mix and first-play
comprehension remain unverified. Do not treat this candidate as publicly cleared.
