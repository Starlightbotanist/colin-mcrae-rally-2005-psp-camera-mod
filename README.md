# Colin McRae Rally 2005 Plus PSP camera mod

An adjustable chase-camera cheat for **Colin McRae Rally 2005 Plus, Europe,
ULES00111 version 1.02**. Change height, distance, base pitch and orientation
follow speed by selecting commented lines in [ULES00111.ini](ULES00111.ini).
The cheat does not change field of view.

Tested with **PPSSPP v1.19.3-660-ga240cb2407** in a single-player Subaru Impreza
start-area fixture. Other game versions and physical PSP hardware are untested.

## Install

1. Copy `ULES00111.ini` to your PPSSPP memory stick's `PSP/Cheats` folder.
   If that file already contains cheats, append this camera block instead of
   replacing the existing file.
2. Enable cheats in PPSSPP and enable **Adjustable chase camera**.
3. Fully restart the game and select either the normal or far chase view.

### Android import

Use **Cheats > Browse** to select the downloaded file. If Android's picker only
shows `.db` files, rename a copy to `camera.db` first; its contents stay the same.
Alternatively, copy the INI directly into the memory stick's `PSP/Cheats` folder.

Save edited files as **UTF-8 without a BOM, with LF (Unix) line endings**.
PPSSPP's Android importer compares the `_S` game-ID line exactly; Windows CRLF
line endings leave an extra carriage return and can cause **No new cheats found
for this game**. The repository enforces LF line endings for the INI.

The running game must be **ULES00111**. Import also skips a cheat whose name is
already present, so that message can mean it was imported previously. Re-import
does not replace an existing camera cheat; edit its installed INI to change it.

Import formatting was checked with PPSSPP's unchanged C++ import functions,
compiled natively on Windows with Android-style newline handling. The original
CRLF file imported no camera codes; the LF file imported all 20 active codes,
preserved an unrelated cheat and skipped a duplicate import. This checks the
importer, not gameplay on an Android device.

## Choose settings with `//`

Keep one height line and one distance line active. For pitch and follow speed,
keep **both lines of exactly one choice** active in each section. Comment the
old choice with `//`, then remove `//` from the desired choice. Labels appear
above the code lines; do not put comments at the end of `_L` lines.

Leave all **FIXED** commands active. Fully restart the game after editing.
To restore stock behavior, disable the camera cheat and fully restart;
disabling a cheat alone does not undo values already written to game memory.

| Setting | Default | Choices |
| --- | --- | --- |
| Height | 2.5 | 0.5 to 5, in steps of 0.25 |
| Distance | 6 | 4 to 12, in steps of 0.5 |
| Base pitch | Down 12.5 degrees | Up 10 to down 30 degrees, in steps of 2.5 |
| Follow divisor | 14, stock | Selected values from 1 to 56 |

Height and distance are offsets from the game's camera origin, not distances
from the roof. Native road and slope compensation remains active. Geometry
choices apply to the low- and high-speed endpoints of both single-player chase
views. Smaller follow divisors catch up faster; larger divisors produce more
lag. This is the game's orientation filter, not independent spring and damping
controls.

## Validation and limits

Controlled tests ran the actual camera functions against identical captured
game memory and registers. Height, distance, pitch and combined geometry were
checked. Increasing base pitch from 8.5 to 12.5 degrees rotated the look direction
by 4 degrees with exactly unchanged camera position. Follow divisors 7, 14 and
28 responded in the expected order to a 30-degree orientation-history error.

The captured vehicle allocation stayed unchanged, and the interior camera's
consumed matrix was identical with and without the edits. PPSSPP's actual cheat
loader applied the selected values, accepted an alternate selection, and
reapplied defaults after loading an older save state. The chase camera retained
its FOV setting of 1.375 in the loader test.

Other cars and tracks, split screen, replays, physical PSP hardware and
controlled performance have not been tested. Instruction guards target the
tested game version; they are not a general compatibility detector. Avoid
combining this with another patch to the same camera parameters or functions.

This adjustable version is for choosing a preferred far-camera preset. It has
not been submitted to the PPSSPP cheat database.
