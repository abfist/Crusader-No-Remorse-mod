# Crusader: No Remorse — Modern Controls

An unofficial Windows mod that adds mouse aiming, modern movement, an equipment wheel, and optional graphics upscaling to **Crusader: No Remorse**.

The mod runs your original game data in a modified native engine, without DOSBox during gameplay. It uses its own launcher and saves. **You must provide your own copy of the game; the installer contains no original game data.**

**Current version:** 0.15 — prototype. Full campaign completion has not been verified.

## Features

- Three selectable movement modes: **Circle Aim**, **Screen**, and **Original**.
- Mouse aiming, left-button firing, and right-button aiming while moving.
- Crouching, aim-relative rolls, and keyboard shortcuts for interactions and equipment.
- A paused equipment wheel showing carried weapons and usable inventory items.
- Updated menus and optional xBRZ graphics upscaling.
- A Windows installer that imports a separate copy of your game data and preserves mod saves and settings during updates.

## Requirements and compatibility

| Requirement | Supported |
| --- | --- |
| Operating system | 64-bit Windows 10 or 11 |
| Game | Crusader: No Remorse |
| Game data for the installer | **English version 1.21** |
| Original DOS saves | Not compatible; start a new game |
| Crusader: No Regret | **Not supported** |

The installer rejects English 1.01, other language/version combinations, and ISO images. It does not download or apply a publisher patch. Update an older copy of your own game to English 1.21 before using the installer.

Players using the installer do not need Visual Studio, CMake, DOSBox, or a separate Visual C++ runtime installation. Development tools are needed only to build from source.

## Install and play

The release installer is named `Crusader-Modern-Controls-0.15-English-1.21-Setup.exe`. Prebuilt installers are separate from the source checkout; the [installer build instructions](#build-the-windows-installer) below produce this file under `dist/`.

1. Run the installer and choose a **separate folder** for Modern Controls.
2. Select your English 1.21 game folder—the folder containing `STATIC`, `USECODE`, and `SOUND`.
3. Complete setup. It verifies the game version and required files, then imports a separate data copy, including `FLICS` when present. Your original installation stays unchanged.
4. Launch **Crusader Modern Controls** from the Start menu or desktop shortcut.
5. Choose **New Game** and a difficulty.

Setup installs for the current Windows user. The default destination is `%LOCALAPPDATA%\Programs\Crusader Modern Controls`. Original DOS saves and configuration are not imported. The release is unsigned.

For unattended installation options, see the [installer readme](installer/README.txt).

## Movement modes

Press **F2 → Enhancements → Movement** to cycle between modes. The change applies immediately and is saved when you close the options.

| Mode | Movement | Aiming |
| --- | --- | --- |
| **Circle Aim** — default | W approaches the aim point; S retreats; A/D circle left/right around it | The aim point stays fixed in the world until you move the mouse. Your character faces it. |
| **Screen** | WASD moves up/left/down/right on screen, facing the direction of travel | Hold right mouse to aim or left mouse to fire toward the pointer. Moving resumes travel-facing after aiming/firing. |
| **Original** | Original arrow/keypad movement and action bindings | Original mouse turning, right-button walking, and left-button firing |

Both modern modes let you aim and fire while moving. In Screen mode, moving the mouse alone does not turn a standing character. A right-click turns without firing; releasing it while stationary keeps that facing. While crouched, both modern modes automatically follow mouse aim.

In Circle Aim, holding A/D maintains distance from the aim point in open space; combining W/S with A/D spirals inward or outward. W stops just short of the aim point. Walls and other collisions still block movement. Combined movement keys do not give a speed boost.

Original mode keeps the mod's menus but restores the original movement and action handling, including Space to fire and Tab/J to jump. F1 displays the original help artwork.

## Controls

These bindings apply to **Circle Aim** and **Screen** unless noted otherwise.

| Control | Action |
| --- | --- |
| WASD | Move according to the selected movement mode |
| Shift + WASD | Run |
| Mouse | Choose or adjust the aim point |
| Left mouse button | Fire; hold for repeated fire |
| Right mouse button | Turn toward the aim point without firing; hold to track; leaves search mode |
| E | Select the nearest searchable object; press again to use or take it |
| F | Select or cycle nearby search targets |
| Left-click in search mode | Use or take the selected object |
| Q | Open or close the equipment wheel |
| R / Shift + R | Next / previous weapon |
| Space | Jump while standing |
| C | Toggle crouch; press again to stand |
| A / D while crouched | Roll once per press |
| Z / X | Roll using the same mapping as crouched A/D |
| I / O | Previous / next inventory item |
| U | Use the selected inventory item |
| M | Use a medikit |
| G | Collect nearby items |
| B | Detonate deployed detpacs |
| Escape | Cancel a selection or open/close the menu |
| F5 / F4 | Quick save / quick load |
| Alt + Enter | Toggle fullscreen |

### Equipment wheel

Tap **Q** to pause gameplay and show the weapons and usable inventory items you carry, with icons, ammunition/quantities, and equipped markers. Click an entry to equip a weapon or select an item. Selecting an item does **not** consume it; press **U** afterward to use it.

Up to eight entries appear per page. Use Previous/Next or Page Up/Page Down for more, or navigate with the arrow keys and Enter. Q, Escape, right-click, or clicking the center cancels. Closing the wheel restores the previous aim point and clears held movement/fire inputs. Original mode retains its original Q binding.

### Crouching and rolling

Crouching stops walking/running. W/S and Space do not move a crouched character; A/D trigger one roll per press. Mouse aiming and left-button firing remain available.

Rolls stay perpendicular to the character's facing. Their sides are mapped from the player's view:

| Character faces | A / Z | D / X |
| --- | --- | --- |
| Up or down | Screen-left | Screen-right |
| Right | Up | Down |
| Left | Down | Up |

Diagonal facings retain diagonal rolls. Each roll keeps its initial direction through the animation; crouched mouse tracking resumes afterward. Release and press again to roll again.

## Graphics and settings

Press **F2 → Enhancements → Graphics Filter** to choose **Upscaled** or **Original**. Upscaled uses xBRZ at a 2×–4× working resolution before fitting the image to the window with its aspect ratio preserved. It smooths existing artwork; it does not add newly drawn detail. Original restores the unfiltered pixel appearance.

Settings are stored in `data/crusader.cfg` inside the mod's installation folder. A developer runtime uses `runtime/data/crusader.cfg` instead.

| Setting | Purpose |
| --- | --- |
| `moderncontrols=true` | Enables the mod's controls and menus; `false` restores the engine's original handling and menus |
| `movementmode=circle`, `screen`, or `original` | Selects movement; Original retains the mod's menus |
| `followplayer=true` | Keeps the player anchored in the view |
| `nativeresolution=false` | Scales the original 640×480 view; `true` shows more scenery |
| `graphicsfilter=xbrz` or `original` | Selects the display filter; the separate `filter` key controls audio |

Keyboard bindings are currently fixed. Leaving the game window releases held inputs and pauses updates.

## Saves, updates, and uninstall

- **Saves:** stored in `data/SAVEGAME` inside the mod installation. Keep them separate from DOS saves and back up progress you want to retain.
- **Updates:** run a newer installer into the same destination. It reuses the imported data and preserves settings and saves without needing the original source folder again.
- **Uninstall:** removes the program, shortcuts, licenses, and bundled source, but leaves the entire `data` folder. Reinstalling to the same destination reuses it.
- **Complete removal:** after backing up wanted saves, delete the remaining data folder manually. Imported data can also remain if setup is cancelled after import.

## Status and known limitations

Version 0.15 adds the Q equipment wheel and R/Shift+R weapon cycling. Release verification passed **eight game test suites** and **36 installer checks**, including installation into a path with Unicode characters, game startup/rendering, unsupported-version rejection, updates, uninstall, reinstall, and preservation of source data/settings/saves. The modern-controls suite passed 13,006 checks.

These are local automated checks and inspected frame captures. A full manual campaign playthrough, clean-machine testing, and every weapon/vehicle have not been validated.

- The underlying community engine is still a work in progress.
- Original sprites have limited facing directions, so movement can look like strafing or sliding even when aim is more precise.
- Missing AVI cutscenes are skipped. Include the available `FLICS` files from your own complete installation for movies.
- F1 describes Original controls; use the table above for the modern modes.
- Keep the original game launcher available as a fallback.

## Build from source

### Requirements

- Windows, PowerShell, and CMake 3.21 or later on `PATH`.
- Visual Studio Build Tools with Visual C++ and the Windows SDK. The scripts default to Visual Studio 2019 and were tested with MSVC 19.29.
- Your own English 1.21 game data for the gameplay and release checks.
- Inno Setup 6.3 or later to compile the installer.

Build scripts download pinned SDL 2.32.10 source if it is missing and verify its SHA-256 checksum. Downloads are cached in `.cache/`.

### Build the Windows installer

Run from the repository root, replacing the example paths with your own:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/package-installer.ps1 -GameData 'C:\Games\Crusader121' -Iscc 'C:\Program Files (x86)\Inno Setup 6\ISCC.exe'
```

Use `-Generator 'Visual Studio 17 2022'` for Visual Studio 2022 in a fresh build tree. The script uses `build/installer`, links SDL and the Visual C++ runtime statically, runs the eight regression suites, and produces:

```text
dist/
  Crusader-Modern-Controls-0.15-English-1.21-Setup.exe
  Crusader-Modern-Controls-0.15-source.zip
  SHA256SUMS.txt
```

The installer also embeds the matching modified source, pinned SDL source, and license notices. Packaging selects source directories explicitly and excludes game data, saves, caches, private files, and Git metadata.

To run installation lifecycle checks:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/test-installer.ps1 -GameData 'C:\Games\Crusader121'
```

The test uses an isolated destination under `artifacts/`, retains logs and a rendered frame, and removes its test program registration afterward. It refuses to run if Modern Controls is already registered for the current Windows user. The source game data is checked for changes.

### Build a developer runtime

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/prepare-game.ps1 -Source 'C:\Games\Crusader121'
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/build.ps1
```

Preparation creates a separate `runtime/data` copy and preserves an existing recognized runtime. Build compiles the game, runs tests, and installs `runtime/crusader-modern.exe`. Start it with **Play Modern Controls.bat** or open the executable directly.

The older preparation script also has a developer-only English 1.01 patching path. That path depends on DOSBox at `original game/DOSBOX/DOSBox.exe`; those game/tool files are not supplied in this repository. The public installer supports already-installed English 1.21 only.

Additional diagnostic commands, run from the repository root:

```powershell
build/Release/modern_controls_tests.exe runtime/data artifacts/modern-controls.png
runtime/crusader-modern.exe --movement-check screen
runtime/crusader-modern.exe --movement-check circle
```

The native movement replays disable autosaving and config writes. Test logs, captures, build outputs, and local game data are excluded from Git.

## License and credits

The engine and mod code are licensed under **GPL-3.0-or-later**. Third-party components retain their respective licenses. See the [GPL license text](engine/LICENSE) and [upstream engine README](engine/README.md).

- **Base engine:** [sebsebseb1982/crusader-no-remorse-decomp](https://github.com/sebsebseb1982/crusader-no-remorse-decomp), based on commit `ec7193218f9a0e590916331f02f6c76891f51fa9`.
- **Graphics, audio, and input:** SDL 2.32.10, under the zlib license. Its source and notice are included in packaged releases.
- **Upscaling:** xBRZ by Zenju. Its [upstream notice](engine/third_party/xbrz/UPSTREAM.md) and [GPLv3 license with the upstream exception](engine/third_party/xbrz/License.txt) are retained.
- **Menu fonts:** Bitstream Vera, with its [font license](engine/assets/menu/fonts/bitstream-vera-license.txt).
- **Menu illustration:** generated with ImageGen; the image source and prompt are in [engine/assets/menu](engine/assets/menu/). Embedded artwork and font atlases can be regenerated with `engine/tools/bake_menu_assets.py` using Python and Pillow. Normal builds use the checked-in assets.

The developer preparation script uses Origin's original 1.21 update, preserved by [Apajalista](https://apajalista.net/id?id=29524), with SHA-256 `4ee927b78deedf22501138c857e178c556a089cbf64ce0dcf67a0caafc1f0d22`. Its script fingerprint matches ScummVM's [1.21 detection record](https://github.com/scummvm/scummvm/blob/master/engines/ultima/detection_tables.h).

Crusader and its original game assets belong to their respective rights holders. This is an unofficial project. The code license does not grant rights to the original game assets.

You can share the mod installer and source with their license notices intact. Do not redistribute `original game/`, `runtime/data/`, or an installed mod's imported `data/` folder. Recipients must provide their own game data. When publishing a repository, check its history as well as its current files; `.gitignore` does not remove previously committed data.
