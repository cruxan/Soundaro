# Changelog

Versions are major.minor.patch. The version is in `Soundaro.csproj`.
Patch: a fix. Minor: a new feature. Major: a big change.

## 2.7.0

Score effects on the cover (they need the online info and the current server):
- **Kill pulse.** When your own score in the server player list goes up, every cover pulses soft red (one breath in 2 seconds, at most 30 % red). Your name and score on the player list turn red and fade back in 4 seconds.
- **Team kill pulse.** When a teammate's score goes up, the cover pulses faint green (at most 15 %). A teammate has the same clan tag as you, or is in your friends list.
- **Join pulse.** When a friend or a teammate joins the server, the cover pulses faint blue (at most 15 %). A player counts as a join only if he or she was not in the list for the last minute, so a short list error does not pulse.
- **Bold scores.** When the score of any player goes up, the name and the score are bold and brighter for 1 to 2 seconds.
- Red comes first, then green, then blue. One switch in Server details, **Pulse on kills**, turns all of this on or off for the profile. It is on by default.
- The player list of the current server is asked every 2 seconds (`ScoresEveryMs` in `ServerWatch.cs`), so an effect comes within about 3 seconds of the event.
- **Who you are.** GMC looks for your name in the player list: the name in the profile, else (Arma 3 only) the Arma 3 profile that was saved last, else the Steam name. A clan tag in front or behind is ignored ("[ABC] Anna", "Anna [ABC]", "ABC | Anna").

The game itself on the cover:
- Next to the totals of the PC, the cover shows the numbers of the game process: on the CPU row how many cores the game keeps busy ("game 4.1 of 16 cores"), on the GPU row the video memory of the game and of the whole card, and on the Memory row the memory of the game. They update once a second. A number that Windows does not give is left out.

Arma 3 only (nothing shows for other games):
- The Server details window has **My mods (loaded now)**: the mods from the `-mod=` part of the start line in the newest game log (RPT), and the log warnings about a mod that needs a missing mod. It shows only while Arma 3 runs, and it only reads the log.

Steam lines:
- Fix: **"Update waiting" was wrong.** Steam keeps the size of the last download in the game manifest after the update is done, so GMC showed a waiting update for an up to date game. An update now waits only when Steam says "update required", or when the download is not finished. The size is what is left.
- **Last played** shows when you left the game, with the time (for example "today 15:56"), not only the day. GMC writes the time when the game closes (`lastexit.txt`). Before the first close, it shows the day from Steam.

Fix:
- **A game that already runs when GMC starts** now starts its profile and its cover. Before, GMC waited for the next start of the game. This matters after a restart of GMC in the middle of a game.

## 2.6.0

- New: **the ping to the connected server on the cover**, at the right edge next to the FPS. It is measured every 3 seconds with a short server query (a round trip), so it is live. It is green up to 100 ms, amber to 200 ms, and red above that. It shows when the FPS is on and the cover finds the current server (the profile needs the online info).

## 2.5.0

- New: **lag alerts.** A game server sends data all the time. When the game still sends packets but nothing comes from the server for 4 seconds, GMC shows "Lag" with a sound. After 12 seconds it shows "Connection lost?". Each stall of 4 seconds or more goes into `lag.csv` (date, time, seconds, server), and the message at the end of a game says how many stalls there were and the longest one. The Game log window has a LAG part.
- It uses only the times of the packets (the network watch), never their content. It needs administrator rights and a profile with the online info that finds the current server. The first 25 seconds after you join a server do not count (loading). When the game stops sending too (a pause, a loading screen), the gap ends and is not a stall.
- The tray menu has a switch "Lag alerts". The numbers (2.5, 4, 12 and 25 seconds) are in `LagLog` in `GameNotes.cs`.

## 2.4.1

- The cover fits long lists and long names without a mouse. With info lines (servers, details, player list, players log) the column is wider (860 instead of 620 at scale 1), and the size still shrinks so that all of it fits the screen. A line that is still too wide gets a smaller font, down to 70 %, and only then "...". Nothing changes place, because the width depends on the profile choices, not on the text.
- The Game log and Server alerts windows can be resized, scroll long lines, and cut long names with "...".

## 2.4.0

- New: **crash notice (Arma 3).** When the game closes, GMC reads its log (`.rpt`). Arma 3 ends the log with "Memory should be free now." only when it closes in the normal way. Without that line, GMC shows a message with the last error line and the number of crashes today, and writes `crashes.csv`. GMC waits until the game process has ended, so the log is complete. When GMC itself ends Arma 3 to join a server, there is no notice.
- New: **FPS of each game.** When a game closes, a message shows the average FPS, the 1 % low and the middle FPS. `fps.csv` also keeps the graphics settings of Arma 3 (view distance, objects, terrain grid, shadows, MSAA, PPAA) and the number of CPU threads, so you can compare runs (for example SMT on and off). This needs the FPS switch of the cover and administrator rights.
- New: **server history.** The servers that you played on, with the time on each (`servers.csv`). It uses the current server that the cover finds, so the profile needs the online info.
- New: **server alerts** (tray menu). Pick a server from your Steam favourites and history, and GMC tells you when a slot is free, when there are at least N players, or when the mission changes or the server restarts. It asks the server every 45 seconds. An alert that fired is removed.
- New: **Game log** window (tray menu): the servers by time, the last visits, the FPS of the last games, and the crashes.

## 2.3.1

- Fix: the cover kept the info of the old server after you joined a new one. Once a sure server was found (from the network or from your name), GMC never looked again, and the old server kept answering. Now GMC looks again every 20 seconds (the network of the last 12 seconds) and switches when you are on another server. A guess never replaces a sure server.

## 2.3.0

- New: **"When that program closes, go back to".** In "When it starts", each profile can name the profile that comes back when its program closes (for example Speakers). The default stays "the profile from before". The choice is grey when "Go back to the earlier profile" is off. If the chosen profile is deleted, GMC uses the profile from before.
- The cover fix of 2.2.1 stays: without any profile to go back to, the cover of a closed program goes away.

## 2.2.1

- Fix: the cover stayed on the screen after the game closed. This happened when GMC started while the game already ran (or started at the same time), because GMC had no profile to go back to. Now the cover of a closed program always goes away.

## 2.2.0

- **The program is called GMC.** The long name, Game Mode Companion, stays in the readme and in the file description. The program file is `GMC.exe`. The settings folder and the autostart entry keep their names, so nothing moves.
- Server tags in plain words (Arma 3): BattlEye, game version, state, locked, signature check, dedicated, platform and mission type. The cover shows a short line. The details window shows one row for each tag, and the raw tags below. Tags with an unknown meaning stay in the raw text.
- Arma 3 mods and DLC: the details window reads the signature key names that the server sends in its rules (checked on a real server). The DLC show their names. The mods show their key names.

## 2.1.2

- Joining a server while Arma 3 runs: the program closes Arma 3 and starts it again on the new server, with the start options of the last start (the mods and the others).
  It asks first: the message says that Arma 3 will be closed, and a second click within 6 seconds is needed. The tray menu and the details window ask in the same way.

## 2.1.1

- Fix: joining a server. Arma 3 does not take Steam's connect address (Steam said "app id specified by server is invalid"), and the query port was used instead of the game port.
  Now Arma 3 is started with `-connect`, `-port` and your own mods when it does not run, and the address is copied when it runs. Other Steam games use the game port of the server.

## 2.1.0

- New: **where my friends play.** The names of your friends are looked for in the player lists of your own servers (Steam favourites and history, up to 10, once a minute).
  The cover shows up to 3 lines with a star, the names and the server. A click joins that server (a second click confirms). The tray menu and the details window list them.
- The query port of a server is now found by itself: Steam can keep the game port, and the server answers on the port next to it. This also helps to find the current server by your name.

## 2.0.0

- **New name: Game Mode Companion** (it was called Soundaro). The program file is `GameModeCompanion.exe`.
  Your settings, banners and logs move by themselves from `%APPDATA%\Soundaro` to `%APPDATA%\GameModeCompanion`. The autostart entry moves too.

- New: **the current server.** Soundaro finds the server that you play on right now. It sees where the game sends its network packets
  (it needs administrator rights, and only listens to the events that Windows reports, never to the content). If that is not possible, it asks your
  recent Steam servers and takes the one that has your name in its player list. The server played last is only the last choice, marked "(guess)".
- New: **all the info of the server**, by its name and not by its address: map, players, bots, ping, type, system, VAC, password, version and tags.
- New: **the player list** on the cover (5, 10 or 20 lines), by score or by time on the server: the name, the team and the score with the time.
  The team is the clan tag in front of the name ("[ABC] Anna"). Your friends (names that you type once) get a star and come first.
  A server does not give the ping of each player, so it is not shown.
- New: **click a server to join it.** A server line on the cover takes the click (only there; the cover still lets the mouse through elsewhere and never takes the focus).
  A second click within 4 seconds joins through Steam. The tray menu has "Join a server", and the details window has "Join this server".
- New: the favourites mode lists up to 5 servers.
- New: the **Server details** window shows everything, including the rules of the server (for Arma 3 the list of mods), with a Copy button.
- Everything in this part connects to the internet, so it works only with the online info switched on.

## 1.9.0

- New: **Players log.** With the online info and a server, Soundaro can log who joins and leaves the server, like a log.
  It asks the server for its player list every 10 seconds (the standard A2S query) and compares the lists.
  It is **off by default**: a profile must switch it on (cover section, "Players log..."). It saves only the name that the server shows, on this PC:
  `players.csv` (date, time, server, joined / left / present, name).
- The cover shows the last 5 events as a log: "20:14:05 + Anna joined", "20:15:30 - Bob left". The lines are reserved, so nothing moves.
- The Players log window shows the list as a log, with the switch, a button to open the file, and a button to delete the list.

## 1.8.0

- New: **Servers on the cover.** Steam keeps your server favourites and history on your PC. The cover can show the server that you played
  last, or your favourites (up to 5), or an own address. Without the online switch, it shows the server names from Steam's file (no network).
  With the online switch on, each line adds the map, the players and the ping.
- The layout reserves the server lines, so nothing moves.

## 1.7.0

- New: **Steam games.** A profile can start on a Steam game: a button next to the program list shows your installed games.
  Soundaro finds the running game through Steam. You can mix Steam games and programs.
- New: **Steam info on the cover** (read from the files of Steam, no network): your Steam play time, when you last played,
  your achievements (for example 22 / 123), and "Update waiting 62 MB" or "Up to date". A switch in the cover section.
- New: **Online info** (off by default, and it connects to the internet): the number of players of the game now (one public call to Valve),
  and one favourite server with name, map, players and ping. A profile must switch it on.
- Fix: the symbols of the two small buttons next to the program list (the list and the Steam game) were not drawn. They are back.

## 1.6.2

- If something unexpected goes wrong, Soundaro shows a window with the details and a "Copy details" button, and you can press Continue.
  It writes no file.
- The once-a-second update of the cover can no longer bring up an error window for a small problem.

## 1.6.1

- Logging is off until you choose it. Before, Soundaro wrote `log.txt` and `playtime.csv` all the time.
  - General settings, "Start and look": "Write a log file (for finding problems)". Off by default.
  - Each profile with programs: "Log the play time of the programs of this profile (and snoozes)". Off by default.
    It writes the play time log, the play time limit with its snoozes, and the game time. A profile without this switch writes nothing about its programs.
- The summary message after a game shows the time of the run. With "Log the play time" on, it also adds up today and the last 7 days.

## 1.6.0

- New: "Look of the cover" (profile section). Colours: Calm (default), Mono, Warm, Night red, Match the profile, or one custom colour.
  What shows: CPU, GPU, memory, clock, game, time left. Graph style: line with fill, bars, or numbers only.
  Place: centre, top left or bottom left (it stays fixed). A limit for the brightness of the text and the graphs.
- New: a small picture in Settings shows the cover with your choices on a made-up screen, also how dark it is.
- New: "Preview on the screens" covers the ticked screens for 8 seconds, also when the profile is not active.
  Choices that you change during the preview show at once. The preview ends by itself, and when Settings closes.

## 1.5.1

- Fix: the cover follows the choices in Settings at once: how dark, the size, the graphs, the FPS and the screens. You do not need to restart Soundaro.
  The darkness changes while you choose it. Cancel puts the old choices back, also on the covered screens.
- The General settings take effect at once, before Save: the sound theme and volume, the messages, the hotkeys, the auto lock and the list of programs
  to never lock. Cancel puts the old ones back. (Start with Windows waits for Save, because Windows asks for a confirmation.)
- Fix: after Cancel in Settings, Soundaro finds the active profile again (each profile has a stable id now), so the timer, the cover and the "back to the earlier profile" step keep working.

## 1.5.0

- New: a summary when a game closes: "Arma 3: 1 h 23 min. Today 2 h 40 min - last 7 days 9 h". It can be switched off.
- New: the play time log has a chart of the last 7 days.
- New: "How dark" for the cover: Black, Very dark, Dark, Dim or Soft dim. A dim cover still shows the screen under it, darker.
- New: Export and Import of profiles (Profiles page). A file with all profiles: a backup, or a way to move them to another PC.
  Import adds the profiles. A name that exists gets a number.

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
  They are made by `tools/make_sounds.py` and sit inside the exe.
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
