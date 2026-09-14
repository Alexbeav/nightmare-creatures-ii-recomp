# Nightmare Creatures II

<!-- retcomm-readme-metrics -->
[![GitHub downloads (all assets, all releases)](https://img.shields.io/github/downloads/Alexbeav/nightmare-creatures-ii-recomp/total)](https://github.com/Alexbeav/nightmare-creatures-ii-recomp/releases)
[![GitHub downloads (latest release)](https://img.shields.io/github/downloads/Alexbeav/nightmare-creatures-ii-recomp/latest/total)](https://github.com/Alexbeav/nightmare-creatures-ii-recomp/releases/latest)
[![GitHub release](https://img.shields.io/github/v/release/Alexbeav/nightmare-creatures-ii-recomp)](https://github.com/Alexbeav/nightmare-creatures-ii-recomp/releases/latest)
<!-- /retcomm-readme-metrics -->

Static recompilation of **Nightmare Creatures II** built on
[psxrecomp](https://github.com/mstan/psxrecomp) and
[recomp-ui](https://github.com/RetroPortingToolKit/recomp-ui).

_Add a short pitch in catalog_identity.json / README._

| | |
|---|---|
| Players | 2 |
| Region | USA |
| Publisher | - |
| Year | - |

Scaffolded with the New Project Layout. See
`psxrecomp/docs/GAME_PROJECT_SETUP.md` for the full flow.

<!-- retcomm-readme-launcher -->
## Retro Launcher

You can run this title **standalone** (release zip + the built-in recomp-ui
Generate & Build flow), or manage installs, updates, ROM/BIOS wiring, and queued
builds more intuitively with
**[Retro Launcher](https://github.com/RetroPortingToolKit/Retro-Launcher)** —
the Retro Compilation Manager hub for self-compiling recomps.

[Downloads](https://github.com/RetroPortingToolKit/Retro-Launcher/releases) ·
[Full README & features](https://github.com/RetroPortingToolKit/Retro-Launcher#readme)

<p align="center">
  <img src="https://raw.githubusercontent.com/RetroPortingToolKit/Retro-Launcher/main/docs/screenshots/hub-and-game-launcher.png" alt="Retro hub with a background build, next to a title’s recomp-ui launcher" width="720">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/RetroPortingToolKit/Retro-Launcher/main/docs/screenshots/queue-and-background-build.png" alt="Background cmake build with titles queued" width="720">
</p>

Retro checks for updates, rebuilds with existing build data when possible,
shares the portable toolchain used by per-title launchers, and automates
BIOS/ROM/save plumbing so you are not stuck repeating each game’s wizard by hand.
<!-- /retcomm-readme-launcher -->

## Diagnostic mode

If the game crashes, freezes, or misbehaves, switch to the diagnostic build
that first-run setup already produced (no recompiling): create an empty file
named `diagnostic-mode.txt` next to `Nightmare_Creatures_II.exe` and start the game as
usual, or run `Nightmare_Creatures_II.exe --diagnostic`. Reproduce the problem, quit, then
run `Nightmare_Creatures_II.exe --collect-diagnostics`: it writes `diagnostics-<date>.zip`
next to the exe. Attach that zip to a GitHub issue on this repository with a
short description of what you did. The zip holds only the runtime's report
files, never saves, BIOS, or disc images. Delete `diagnostic-mode.txt` to go
back to normal mode. Details: `psxrecomp/docs/DIAGNOSTIC_MODE.md`.

## Legal

You must own the original game. Disc images under `disc/` are gitignored and
must never be committed. Retail BIOS dumps are not redistributed and OpenBIOS is
not shipped: this title is retail-BIOS-only, so first-run Generate needs your own
legally dumped SCPH-1001 image.

Default app icon: `assets/psxrecomp.ico` (and `.png` / `.svg`) — Retro-themed controller mark from `psxrecomp/assets/`. Windows builds embed it via `APP_ICON`.

Box art is not shipped in this kit or its repository. Redistribution permission for third-party cover images is unresolved, so the launcher runs without one.

## Quick start (dev)

```bash
git submodule update --init --recursive
./psxrecomp/tools/ci/build_emitters.sh
python3 psxrecomp/psxrecomp_cli.py generate \
  --config game.toml --project-root . --disc disc/<your>.cue
cmake -S . -B build-release -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build-release --target psx-runtime
```

Zip prefix for CI artifacts: `nightmarecreaturesii`.

## Symbols

Progressive map: `symbols.toml` → `python3 tools/sync_symbols.py` →
`psx_symbols.h` (`PSX_FN_*`). See `psxrecomp/docs/SYMBOLS.md`.

## Framework pins

Submodule gitlinks (`psxrecomp`, optional `recomp-ui`, nested `recomp-net`)
are authoritative. `framework_pins.txt` is an optional scaffold snapshot;
release CI logs SHAs with `record_pins.sh` but builds whatever the gitlinks
resolve to. Bump submodules deliberately — do not float on `main`/`master`
in release CI.

<!-- retcomm-readme-raid -->
---

<p align="center">
  <sub><b>R.A.I.D. — Retro AI Development</b> · a Discord for AI-assisted retro reverse-engineering, decomp &amp; recomp</sub>
</p>

<p align="center">
  <a href="https://discord.gg/Ad9BwSzctP"><img src=".github/raid-discord.png" alt="Join the Retro AI Development (R.A.I.D.) Discord" width="200"></a>
</p>
<!-- /retcomm-readme-raid -->
