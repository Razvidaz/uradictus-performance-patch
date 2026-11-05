# Uradictus Performance Patch

A performance patch for **Europa Universalis IV 1.37.5** on Windows. It makes long and large games run smoother: fewer
freezes when you click windows and armies, shorter month-start stutters, smoother pictures on busy days, and a faster
boot. It works in single player and multiplayer. Other players don't need it.

## ⬇️ [Download the patch (uradictus-performance-patch-1.37.5.zip)](https://github.com/Razvidaz/uradictus-performance-patch/releases/latest/download/uradictus-performance-patch-1.37.5.zip)

The link always gets the newest version. The zip holds `version.dll` and `README.txt`.

## Requirements

- Europa Universalis IV **1.37.5** exactly (the Steam default branch).
  `eu4.exe` MD5: `5af10c50faebd12408149a3a27deffcb`. On any other version the patch does nothing.
- Windows 10 or 11, 64-bit.

## Install

1. Close EU4.
2. In Steam: right-click **Europa Universalis IV** > **Manage** > **Browse local files**. This opens the folder with
   `eu4.exe`.
3. Unzip the download and copy `version.dll` into that folder, next to `eu4.exe`.
   If a `version.dll` is already there (another tool uses the same name), move it out of the game folder first. Only
   one can be installed.
4. Start the game as usual.

Windows or your antivirus may warn about `version.dll` because it's an unsigned file that loads into the game. You can
compare the file with the SHA-256 listed on the release page.

## Use

A small window shows on top of the game:

- **Performance ON / OFF:** switches every speed-up on or off during play. A change waits until the current game day
  has finished. The patch starts **on** every time the game launches.
- **Speed 4:** how many days per second game speed 4 runs, from 2.0 to 5.0 (5.0 is the game's own). It starts at 2.5
  every launch. Only the host, or you in single player, can change it; for a multiplayer client it's greyed out,
  because clients always follow the host's pace.
- **F10** closes or opens this window. Closing it doesn't switch anything off.

Drag the window by its title to move it. If exclusive fullscreen hides it, use windowed or borderless mode.

## What it speeds up

- Interface updates: the top bar, alerts and outliner refresh less often; Paradox online services run less often.
- More pictures during long game days, the monthly ranking, the monthly country and unit steps, and after peace deals.
- Textures and music: loaded before you need them and kept loaded, so windows open faster the first time and stay fast.
- Faster file lookups at boot and while playing.
- Big armies and fleets: unit panels, multi-army selections, fleet movement estimates, trade mission node lists and
  closing windows.
- A fix for a game bug where open province windows leak interface elements, which slows long sessions down.
- Faster game calculations: army drill in expenses, reinforcement and morale, fleet speed, modifier merging, AI war goals
  and invasion planning. Each one gives the same answers as the game and checks itself against the game's own code
  now and then; a difference turns it off.
- Multiplayer: Steam messages are sent without the game's extra buffering, and clients skip rebuilding the parts of
  the daily sync check that can't cause an out-of-sync.

Measured in long games on 1.37.5 with the patch on:

| | Without | With |
|---|---|---|
| Boot to main menu | ~49 s | ~32 s |
| Window and tab clicks, average | 79 ms | 18 ms |
| Worst frame while paused | 644 ms | 144 ms |
| Selecting a 3000-regiment army | 360-455 ms | 27-45 ms |
| Month-start ranking freeze | 235-260 ms | 58-106 ms |

## Multiplayer

- Everyone can install it, or only some players. Players without it aren't affected.
- The patch never sends orders and never changes the game's rules. Its calculations give the game's own answers.
- If you ever see an out-of-sync that you think the patch caused, switch Performance off and report it (see below).

## Files it writes

Both in the game folder:

- `eu4perf.log`: what the patch did this session.
- `eu4perf_textures.txt`: the textures to load in advance. It starts with a list made on the Tuesday HAB mod and adjusts
  to your game as you play: textures your game opens are added, names your game doesn't have are removed. Delete it
  to start over.

## Remove

Close EU4 and delete `version.dll`, `eu4perf.log` and `eu4perf_textures.txt` from the game folder. If you moved another
`version.dll` out before installing, put it back. Your game files and saves are never changed.

## Problems

Open an [issue](../../issues) with what happened, your game version, and the `eu4perf.log` file from the game folder.



> Unofficial. Not made or supported by Paradox Interactive.
