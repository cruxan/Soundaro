# Changelog

Versions are major.minor.patch.
Patch: a fix. Minor: a new feature. Major: a big change.

## 1.4.0

- New: a play time log. Each time a program of a profile runs and closes, one line goes to `%APPDATA%\Soundaro\playtime.csv`
  (date, start, end, seconds, profile, program). It opens in Excel or Notepad.
- New: a profile can have several programs (separate them with commas). The list button adds the chosen program to the list.
  The profile starts when one of its programs starts, and it counts as closed when all of them closed.
- New: in Settings, a section "Play time log" shows the time of all programs of the profile, added up: today, the last 7 days and in total,
  by program, and the last sessions. A button opens the log file.

## 1.3.0

- New: sounds that sound like a real product. Three themes: Glass bell (default), Marimba and Soft pluck. Or Off.
  Seven sounds: profile switch, time is up, snooze, mute on, mute off, mouse lock, mouse free.
  They are made for Soundaro and sit inside the exe.
- New: in Settings, General, Messages and sound: a theme choice and a button for every sound. A new theme plays at once.
- New: sounds for the mute and mouse lock hotkeys (the auto lock stays silent). One switch turns them off.

## 1.2.1

- The play time limit can be 5 to 480 minutes (before: 15 to 240). Each profile remembers its own limit.

## 1.2.0

- New: a play time limit for each profile (5 to 480 minutes). It starts with the profile.
  The cover shows the time that is left. When the time is up, a message shows, a soft sound plays, and the covered screens pulse slowly
  (black to a dim amber, one breath in 4 seconds, never bright). A plain black cover pulses too.
- New: the tray menu has "Snooze 10 minutes" and "Stop the play time reminder" while a timer runs.
- New: the log has the play time (start, time up, each snooze, end) and the game time of each program (how long it ran).

## 1.1.1

- Fix: with the graphs switched off, the cover is plain black. Before, it still drew the profile name, the clock and empty graph frames.

## 1.1.0

- New: a profile can cover chosen screens with black, to remove the glare. The main screen is never covered.
  The cover never takes the focus, and mouse clicks go through it.
- New: the cover can show CPU, GPU and memory graphs, the game name, and the game picture.
  The picture is the Steam picture of the game, or the icon of the program. Soundaro reads both from the disk only.
- New: the cover can show the FPS and the 1 % low of the game. This needs Soundaro to run as administrator.
  The tray menu has "Restart as administrator". Games with DirectX 9 to 12 work. Vulkan and OpenGL games may show no FPS.
- The tray menu has "Remove the black cover".
- The cover goes away first when a game closes, before the sound switches. The program check runs every 1.5 seconds.
- The FPS shows the median too. One missed reading keeps the last number for 3 seconds.
- New: Settings, General: "As administrator" starts Soundaro as administrator at sign-in (a scheduled task, no question at sign-in). The FPS needs it.
- New look for Settings: a soft header band with the logo, pill tabs, section cards with an icon and a short summary, a slide when a section opens, switches instead of tick boxes, rounded fields, bigger profile rows with a glowing dot for the active profile, and soft buttons that fade on hover.
- A profile whose game has a Steam picture shows the game banner at the top of the profile. Soundaro saves a copy of the banner when it first sees the game run. Nothing goes to the network.
- Settings: the "Hotkey that frees the mouse" box is gone. The lock hotkey already frees the mouse. A key that was set before keeps working.
- Fix: the median and the 1 % low of the FPS showed huge numbers. They now use the time stamp that Windows puts on each frame.
- Fix: a game counts as closed when its window is gone. Before, Soundaro waited until the process ended, and a game can need 15 seconds for that. The black cover and the profile switch now come in about 3 seconds.
- Fix: the Steam picture path was cut one letter short, so no Steam picture loaded.
- The profile list shows the real icon of the program of a profile, when Soundaro has seen the program run. Soundaro keeps a small copy of each program icon.
- A profile without a known program (headphones, speakers) gets a banner with its own icon and its playback device, on a gradient in a colour for that icon.
- Soundaro looks for the program of each profile in the Steam library folders at start, so the banner and the icon are there before the game ever ran.
- The banner follows the theme: a light banner with dark text in the light theme. Before it was too dark there.
- A program without a Steam picture gets a banner too: its icon (never enlarged, so it stays sharp) on a soft gradient in the main colour of the icon.
- Settings: the Profiles page and the General page have sections that open and close. One section is open at a time, so no page needs scrolling.
- The program name field has a small list button: choose from the running programs. It is not a file picker.
- New: a size for the cover text and graphs: small, medium or large. The size follows the screen (4K, portrait) and always fits on it.
- Nothing on the cover changes place. Only the graphs and the numbers move.

## 1.0.4

- Fix: Settings shows the active profile after Soundaro starts, before the first jump.

## 1.0.3

- Fix: a volume that a profile sets is temporary. The volume from before comes back when you switch to a profile that sets no volume.

## 1.0.2

- Fix: a profile that does not mute now always unmutes the speakers and the microphone.

## 1.0.1

- The blue highlight in the profile list follows the active profile.

## 1.0.0

First release.

- Sound profiles with one hotkey, start on program, start on device connect.
- Mute profile: mutes the speakers and the microphone.
- Mouse lock with auto detect, hotkeys to lock, free and switch auto on and off.
- Per-game tools: mute when away, push to talk, mouse speed.
- Settings shows the active profile and the recent jumps.
- A profile does not jump back by itself after our own switch.
