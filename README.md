# Bubble Memories – Background Editor

A Windows tool that changes the level backgrounds of **Bubble Memories: The Story Of Bubble Bobble III** (Taito, 1995) directly inside your **MAME ROM zip**.

For every level you can:

- **keep** the original background,
- **remove** it (black background, like the original Bubble Bobble),
- use a **color** of your choice, optionally semi-transparent to tint the original background,
- use your own **image** (PNG, JPG, GIF, BMP, WebP).

The tool edits the ROM files only. MAME itself is never touched, and the modified game runs in a standard MAME.

> **No ROMs are included.** You need your own MAME romset of the game.

## Download

Download tool from this repository.

It is a **portable** program: no installation is needed. Put it anywhere, for example on a USB stick, and double-click it. The first start takes a few seconds while it unpacks itself.

**Windows SmartScreen:** the executable is not digitally signed, so the first time Windows may show *"Windows protected your PC"*. Click **More info → Run anyway**.

## Requirements

- Windows 10 or 11, 64-bit
- A MAME romset of Bubble Memories in `.zip` format (`.7z` is not supported)

## Supported versions

| MAME set | Game |
| --- | --- |
| `bubblem` | Bubble Memories: The Story Of Bubble Bobble III (Ver 2.4O 1996/02/15) – World |
| `bubblemu` | Bubble Memories: The Story Of Bubble Bobble III (Ver 2.5A 1996/02/21) – USA |
| `bubblemj` | Bubble Memories: The Story Of Bubble Bobble III (Ver 2.3J 1996/02/07) – Japan |

The files are recognized by their content (checksums), not by their names. This means *merged*, *split* and *non-merged* romsets all work. The default EEPROM files (`.nv`) are not needed. The tool was tested with MAME 0.288.

## How to use

1. Click **Open ROM…** and choose your zip.
   - With a *merged* romset this is `bubblem.zip`, which contains every version. The World version is selected by default.
   - With a *split* romset you can open the game's own zip (for example `bubblemu.zip`), as long as the parent `bubblem.zip` is in the same folder.
2. If the zip contains more than one version, pick one in **Version**.
3. Select one or more levels in the list on the left:
   - click a level to select it;
   - use Ctrl+click or Shift+click to select several;
   - click a group title to select the whole group.
4. Choose what to do with the background: **Original**, **Remove**, **Color** or **Image**.
   - **Color:** pick a color and set its opacity. Below 100% the color tints the original background.
   - **Image:** choose a file or drag it onto the preview. Pick how it fits the screen (*Fill*, *Fit*, *Stretch*) and whether to use *Dithering*.
5. Optionally apply the same choice to **the whole group** or to **all levels**.
6. Click **Save ROM**.

The preview on the right shows exactly what you will see in the game. The thumbnails on the left show each level's original background. A small inset appears on modified levels; hover over it to swap before and after.

The list has 192 levels, in playing order:

- **Story**: rounds 1–80, in groups of 10, and the 6 secret rooms;
- **Practice game**: the 10 practice rounds;
- **Super**: the 80 rounds of Super mode, which has other stage layouts and the same backgrounds in a different order, and its 6 secret rooms;
- **Super practice game**: the 10 practice rounds of Super mode.

Every level is separate: changing round 1 of Story does not change round 1 of Super. Under the level name you can see which of the 25 original backgrounds it uses, so you can tell which levels share one.

### Saving

- **Save as new zip** creates a complete zip of the selected version. For the USA and Japan versions this is `bubblemu.zip` or `bubblemj.zip`: put it in your MAME `roms` folder. MAME looks for the game's own zip before the parent zip, so this works next to your original romset, which stays untouched.
  The World version is the parent set, so its zip is `bubblem.zip`, the same name as your romset. If the new zip would replace a `bubblem.zip` that also holds the other versions, the tool asks first: those versions would no longer be in it (the original is kept as a `.bak` copy).
- **Modify the open zip** changes the zip you opened and keeps its structure. It first makes a backup copy with the `.bak` extension. In a merged romset every version inside the zip is updated consistently. This is the easiest choice for the World version of a merged romset. **Restore the original** puts the zip back from the backup.

Use **Project → Save project…** and **Load project…** to keep your choices and apply them again later, even to a romset of another version.

## Running the modified game in MAME

- The game starts normally, from the MAME menu as well as from the command line. `mame -verifyroms` reports the set as *good*.
- While the game loads, MAME shows a **red warning** saying that some ROMs are incorrect. This is expected for a modified ROM: press any key to continue.
- Romset managers (ClrMamePro, RomVault…) may treat the modified files as wrong or "fix" them. Keep the modified zip out of folders you rebuild or fix with those tools, and keep the `.bak` copy.

## Limits

- Each image is converted to 320×224 pixels with up to 93 colors (3 palettes of 31 colors, chosen tile by tile): the same limit as the game's own backgrounds. Transparent parts of an image become black.
- New pictures are stored in graphics tiles. The graphics chips have **988** free tiles, and a detailed image uses about 280, so roughly **3 different images** fit at first.
  - Levels that use the same image share it.
  - Black and opaque colors use no tiles at all.
  - When every level that uses an original background gets a new one (black, a color or an image), the tiles of that background become free for new pictures: about 300 each. **Remove all backgrounds** frees about 6,400 tiles, enough for about 20 more images.
  - A semi-transparent color is stored like an image, one for each different original background.
  - The bar at the bottom of the window shows how much space is left.
- With a *split* romset opened from `bubblem.zip`, the USA and Japan zips next to it read their graphics from `bubblem.zip` and still show the original backgrounds. In that case only the 988 free tiles can be used, and the tool says so under the zip name.
- Some rounds change the background on purpose, and they do it with yours too: round 38, for example, shows it with a light blue veil. In many rounds, especially in Super mode, the walls of the stage cover most of the screen.

## Disclaimer

This is an unofficial fan tool. It is not affiliated with or endorsed by Taito or the MAME team. *Bubble Memories* and *Bubble Bobble* are trademarks of their respective owners. ROM images are copyrighted: use only ROMs you are legally entitled to use. The tool works entirely offline and does not collect or send any data.
