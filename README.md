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
- Big armies and fleets: unit panels, multi-army selections, fleet movement estimates, trade mission node lists,
  route checks while you hover the map with a unit selected (up to ~130 ms per frame with a big army before), and
  closing windows.
- A fix for a game bug where open province windows leak interface elements, which slows long sessions down.
- Single player: the game keeps drawing while the AI thinks each day, instead of freezing until the slowest country is
  done (new in 1.4).
- Faster game calculations: army drill in expenses, reinforcement and morale, fleet speed, modifier merging, AI war goals,
  AI threat lookups (new in 1.4) and invasion planning. Each one gives the same answers as the game and checks itself
  against the game's own code now and then; a difference turns it off.
- Multiplayer: clients send their own orders without the game's extra Steam buffering and skip rebuilding the parts of
  the daily sync check that can't cause an out-of-sync. The host sends the game's own way, and from 1.4 works out and
  sends only the part of that daily sync list that can start an out-of-sync (see [Hosting](#hosting)).

Measured in long games on 1.37.5 with the patch on:

| | Without | With |
|---|---|---|
| Boot to main menu | ~49 s | ~32 s |
| Window and tab clicks, average | 79 ms | 18 ms |
| Worst frame while paused | 644 ms | 144 ms |
| Selecting a 3000-regiment army | 360-455 ms | 27-45 ms |
| Month-start ranking freeze | 235-260 ms | 58-106 ms |

Switched off and on in one session (1764 save, speed 3):

| | Off | On |
|---|---|---|
| Average fps | 36 | 81 |
| Longest frame | 651 ms | 48 ms |
| Selecting an army | 220-651 ms | 20-38 ms |
| Worst frame at a month start | 119-200 ms | 30-48 ms |

## If your antivirus deletes it

Some antivirus programs flag `version.dll` because it is unsigned, has no download history yet, and loads itself into
the game, which is also what some malware does. If it disappears or is blocked:

1. **Windows Defender / Windows Security:**
   - Already deleted: open **Windows Security** > **Virus & threat protection** > **Protection history**, click the
     entry for `version.dll`, then **Actions** > **Allow on device** (or **Restore**).
   - So it doesn't happen again: **Virus & threat protection** > **Manage settings** (under Virus & threat protection
     settings) > **Exclusions** > **Add or remove exclusions** > **Add an exclusion** > **File**, and pick
     `version.dll` in the game folder.
2. **Other antivirus** (Avast, AVG, Bitdefender, Norton, Kaspersky and others): open its settings, find
   **Exceptions** or **Exclusions**, and add the full path of the file, usually
   `C:\Program Files (x86)\Steam\steamapps\common\Europa Universalis IV\version.dll`. If it was moved to quarantine,
   restore it from there first.
3. If your browser blocks the download, choose **Keep** in its downloads list.

Exclude only this one file, not the whole game folder or drive.

## Multiplayer

- Everyone can install it, or only some players. Players without it aren't affected.
- The patch never sends orders and never changes the game's rules. Its calculations give the game's own answers.
- If you ever see an out-of-sync that you think the patch caused, switch Performance off and report it (see below).

### Hosting

When you host, the daily sync list you send carries only the numbers that can start an out-of-sync; the other 137 are
sent as 0. This saves the host up to about 80 ms every game day in big games, and the host sets everyone's pace. Other
players don't need the patch. The cost: if a real out-of-sync happens, its report can't show which part of the game
split first. After any player reports an out-of-sync, the full list goes out for the rest of that session. Tell the
other players before you host with it.

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
