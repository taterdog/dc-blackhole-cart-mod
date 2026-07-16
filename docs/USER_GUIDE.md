# Data Center Black-Hole Cart User Guide

This guide explains how to install, confirm, use, configure, and troubleshoot
Data Center Black-Hole Cart.

The guide is written for players. You do not need to build anything from
source unless you are developing the mod.

## Contents

- [Start Here](#start-here)
- [Read This Before Using It](#read-this-before-using-it)
- [Files You Need](#files-you-need)
- [Install Checklist](#install-checklist)
- [Find The Data Center Folder](#find-the-data-center-folder)
- [Install MelonLoader](#install-melonloader)
- [Install The Mod](#install-the-mod)
- [Confirm It Loaded](#confirm-it-loaded)
- [Use The Cart](#use-the-cart)
- [Config](#config)
- [Troubleshooting](#troubleshooting)
- [Bug Reports](#bug-reports)
- [Uninstall](#uninstall)
- [Build From Source](#build-from-source)

## Start Here

Data Center Black-Hole Cart changes the cart in **Data Center** into a
hidden inventory.

The basic loop is simple:

1. Hold an item.
2. Walk to the cart.
3. Press `E` to store the item.
4. Empty your hands.
5. Press `E` on the cart to open the cart menu.
6. Click an item in the menu to take it back out.

The cart menu also has:

- `Collect`, which pulls eligible nearby or purchased items into the cart.
- Search, so you can filter the list.
- Name sorting, so you can flip between `Name A-Z` and `Name Z-A`.
- A scrollbar for larger cart inventories.
- A red `X` on each row for deleting trash after confirmation.

## Read This Before Using It

Cart contents persist per Data Center save file.

Cart contents are committed only when Data Center saves the game. If you add or
remove cart items and then quit or load another save without saving, those cart
changes are discarded just like unsaved game-world changes.

When you load a different save, the mod clears the current live cart objects and
loads that save's own last-saved black-hole cart inventory. This prevents items
from one save appearing in another save.

Before using any mod on an important save, make a backup using your normal
Steam or game backup method.

## What The Mod Preserves

The mod stores the live game object while the current game session is running.
When Data Center saves the game, the mod writes a per-save persistence record
under `UserData/DataCenterBlackHoleCart/Saves/`. After a save loads, stored cart
items are reconstructed from that record.

State preserved while an item is stored includes:

- network switch configuration;
- switch VLAN filter settings where the game exposes them;
- installed SFP/QSFP modules on switches;
- SFP/QSFP box type and used slots;
- compatible loose SFP/QSFP modules merged into boxes;
- cable spool remaining length;
- other fields stored on the original game object.

The menu also cleans up common display noise:

- item names do not show the Unity `(Clone)` suffix;
- SFP/QSFP boxes show counts such as `3/5 SFPs`;
- cable rolls show their remaining length.

## Files You Need

The release ZIP contains documentation plus the two mod files.

Only these two files go into the game's `Mods` folder:

```text
DataCenterBlackHoleCart.dll
DataCenterBlackHoleCart.deps.json
```

Do not put the whole ZIP, the whole source folder, or the `docs` folder inside
`Mods`.

## Install Checklist

Use this checklist if you already know where your Data Center folder is.

1. Close Data Center.
2. Install MelonLoader into the Data Center game folder.
3. Start Data Center once with MelonLoader installed.
4. Quit Data Center after it reaches the main menu.
5. Copy `DataCenterBlackHoleCart.dll` and
   `DataCenterBlackHoleCart.deps.json` into `<Data Center>/Mods/`.
6. Start Data Center through Steam.
7. Load a save, walk to the cart with empty hands, and press `E`.

If the cart menu opens, the mod is installed.

## Persistent Cart Files

The mod stores per-save cart inventory files here:

```text
<Data Center>/UserData/DataCenterBlackHoleCart/Saves/
```

Each file is tied to one Data Center save name and represents the cart state at
the last successful Data Center save command. You normally do not need to edit
these files. If you back up a save and want the cart inventory too, back up this
folder along with the game's normal save data.

## Find The Data Center Folder

The Data Center game folder is the folder that contains:

```text
Data Center.exe
Data Center_Data/
```

After MelonLoader is installed, the same folder should also contain:

```text
MelonLoader/
Mods/
Plugins/
UserData/
version.dll
```

### Best Method: Steam

This works on Windows and Linux:

1. Open Steam.
2. Go to `Library`.
3. Right-click `Data Center`.
4. Choose `Manage`.
5. Choose `Browse local files`.

The folder that opens is the folder you need.

### Common Windows Locations

Default Steam library:

```text
C:\Program Files (x86)\Steam\steamapps\common\Data Center
```

Custom Steam library example:

```text
D:\SteamLibrary\steamapps\common\Data Center
```

### Common Linux Locations

Normal Steam install:

```text
~/.local/share/Steam/steamapps/common/Data Center
```

Older Steam path:

```text
~/.steam/steam/steamapps/common/Data Center
```

Steam Flatpak path:

```text
~/.var/app/com.valvesoftware.Steam/.local/share/Steam/steamapps/common/Data Center
```

If you are unsure, use Steam's `Browse local files` button.

## Install MelonLoader

Data Center is a Unity IL2CPP game. MelonLoader must be installed before this
mod can load.

Useful links:

- MelonLoader releases: <https://github.com/LavaGang/MelonLoader/releases>
- MelonLoader wiki: <https://melonwiki.xyz/>
- .NET 6 downloads: <https://dotnet.microsoft.com/en-us/download/dotnet/6.0>
- .NET Linux install docs: <https://learn.microsoft.com/en-us/dotnet/core/install/linux>

This mod has been tested with MelonLoader `0.7.3`. Use `0.7.3` or newer unless
a release note says otherwise.

### Windows

Recommended path:

1. Close Data Center.
2. Download `MelonLoader.Installer.exe` from the MelonLoader releases page.
3. Run the installer.
4. Select `Data Center.exe` inside the Data Center game folder.
5. Install MelonLoader.
6. Start Data Center once through Steam.
7. Quit after the game reaches the main menu.

If the installer does not work, use the manual Windows ZIP from the MelonLoader
release page and extract its contents into the Data Center game folder.

### Linux / Steam Proton

1. Close Data Center.
2. Find the game folder with Steam's `Browse local files`.
3. Download `MelonLoader.Installer.Linux` from the MelonLoader releases page.
4. Make it executable:

```bash
chmod +x MelonLoader.Installer.Linux
```

5. Run it:

```bash
./MelonLoader.Installer.Linux
```

6. Select `Data Center.exe`.
7. Install MelonLoader.
8. Start Data Center once through Steam.
9. Quit after the game reaches the main menu.

For Steam Flatpak, the installer may need access to the Flatpak Steam library:

```text
~/.var/app/com.valvesoftware.Steam/.local/share/Steam/steamapps/common/Data Center
```

If the installer cannot access that folder, adjust Flatpak permissions with
your desktop's Flatpak permission tool or Flatseal.

## Install The Mod

Install the mod only after MelonLoader is installed and Data Center has been
launched once with MelonLoader.

1. Close Data Center.
2. Open the mod release ZIP.
3. Copy these two files:

```text
DataCenterBlackHoleCart.dll
DataCenterBlackHoleCart.deps.json
```

4. Paste them into:

```text
<Data Center>/Mods/
```

The finished layout should look like this:

```text
Data Center/
  Data Center.exe
  Data Center_Data/
  MelonLoader/
  Mods/
    DataCenterBlackHoleCart.dll
    DataCenterBlackHoleCart.deps.json
  UserData/
```

Start Data Center through Steam when the files are in place.

## Confirm It Loaded

### In Game

1. Load a save.
2. Walk to the cart.
3. Make sure your hands are empty.
4. Press `E`.

The black-hole cart menu should open. It can open even when it is empty.

### In The Log

Open:

```text
<Data Center>/MelonLoader/Latest.log
```

Look for lines like:

```text
Melon Assembly loaded: '.\Mods\DataCenterBlackHoleCart.dll'
Data Center Black-Hole Cart loaded.
Black-hole cart config loaded:
Support Module Loaded
```

If those lines are present, MelonLoader found the mod and the mod started.

## Use The Cart

### Store One Item

1. Pick up an item.
2. Walk close enough to interact with the cart.
3. Press `E`.

The item disappears from your hands and is stored in the cart.

### Open The Cart Menu

1. Empty your hands.
2. Walk close enough to interact with the cart.
3. Press `E`.

The cart menu opens.

### Take An Item Out

1. Open the cart menu.
2. Click the item row.

The menu closes and the item is placed in your hands.

### Collect Items

Open the cart menu and click `Collect`.

`Collect` can pull in:

- loose physical items near the active cart;
- items already sitting on the cart;
- purchased shop or storage items that the game has loaded;
- non-empty SFP/QSFP boxes;
- loose compatible SFP/QSFP modules, when they can be handled safely.

The default loose-item range is `10` meters from the active cart. You can
change this in the config file.

`Collect` intentionally avoids:

- items currently in your hands;
- items already in the black-hole cart;
- rack-installed items;
- SFP/QSFP modules still in a box, installed in a port, or attached to cable;
- protected unpurchased shop stock.

### Search, Sort, And Scroll

- Use the search field to filter visible items.
- Use the sort button to switch between `Name A-Z` and `Name Z-A`.
- Use the mouse wheel or scrollbar when the list is longer than the menu.

### Delete Trash

1. Click the red `X` on an item row.
2. Confirm deletion.

Deleting destroys the stored item. Use it only for trash.

## Config

The mod creates this file the first time it loads:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

Close Data Center before editing the file. Restart the game after saving
changes.

Default config:

```text
BulkPickupRadiusMeters = 10
SortDescendingDefault = false
CartWheelColor = #FF69B4
CartFrameColor = #00FF00
CartPlatformTrimColor = #000000
CartColor = none
MenuWidthRatio = 0.54
MenuHeightRatio = 0.76
MenuMaximumWidth = 980
ItemRowHeight = 70
TitleFontSize = 34
HeaderFontSize = 28
ItemFontSize = 30
SearchFontSize = 28
ButtonFontSize = 28
```

### Common Changes

Make `Collect` reach farther:

```text
BulkPickupRadiusMeters = 15
```

Make the list rows taller:

```text
ItemRowHeight = 82
```

Make item text larger:

```text
ItemFontSize = 34
```

Start sorted Z-A instead of A-Z:

```text
SortDescendingDefault = true
```

Change the frame color:

```text
CartFrameColor = #00FF00
```

Change the platform/trim color:

```text
CartPlatformTrimColor = #000000
```

Change the wheel color:

```text
CartWheelColor = #FF69B4
```

Leave one cart part's original game color alone:

```text
CartWheelColor = none
```

### Config Reference

`BulkPickupRadiusMeters`

How far `Collect` reaches for loose ground items near the active cart. The
mod clamps this between `0` and `100`.

`SortDescendingDefault`

If `true`, the cart menu starts in `Name Z-A` order. If `false`, it starts in
`Name A-Z` order.

`CartWheelColor`

Tint applied to the cart wheels. Use `#RRGGBB`, `#RRGGBBAA`, `RRGGBB`,
or `RRGGBBAA`. Short forms such as `#123` are also accepted. Set this to
`none`, `off`, `original`, or `default` to leave the original wheel material
color alone.

`CartFrameColor`

Tint applied to the original white cart frame. Uses the same color formats
as `CartWheelColor`.

`CartPlatformTrimColor`

Tint applied to the original red cart platform/trim. Uses the same color
formats as `CartWheelColor`. The shorter config aliases `CartPlatformColor`
and `CartTrimColor` are also accepted.

`CartColor`

Fallback tint for cart materials the mod cannot identify as a wheel, frame, or
platform/trim. Leave this as `none` unless one cart part is not being matched.
Uses the same color formats as `CartWheelColor`.

`MenuWidthRatio`

How much of the screen width the menu tries to use. The mod clamps this between
`0.25` and `0.95`.

`MenuHeightRatio`

How much of the screen height the menu tries to use. The mod clamps this
between `0.25` and `0.95`.

`MenuMaximumWidth`

Maximum menu width in pixels. The mod clamps this between `360` and `2400`.

`ItemRowHeight`

Height of item rows in pixels. Increase this if text feels cramped. The mod
clamps this between `44` and `140`.

`TitleFontSize`, `HeaderFontSize`, `ItemFontSize`, `SearchFontSize`,
`ButtonFontSize`

Menu font sizes. The mod clamps these between `14` and `80` for title text and
between `14` and `72` for the other font sizes.

## Troubleshooting

Start with the symptom that matches what you see.

### The Cart Acts Like The Normal Game Cart

Likely causes:

- the mod files are in the wrong folder;
- Data Center was not restarted after install;
- MelonLoader is installed in a different game folder than the one Steam runs;
- MelonLoader did not load successfully.

Check:

1. `DataCenterBlackHoleCart.dll` is directly inside `<Data Center>/Mods/`.
2. `DataCenterBlackHoleCart.deps.json` is directly inside `<Data Center>/Mods/`.
3. The files are not inside `<Data Center>/Mods/DataCenterBlackHoleCart/`.
4. `MelonLoader/Latest.log` contains `Data Center Black-Hole Cart loaded.`

### There Is No Mods Folder

MelonLoader is not installed, or Data Center has not been launched once after
installing MelonLoader.

Fix:

1. Install MelonLoader into the Data Center folder.
2. Launch Data Center once.
3. Quit the game.
4. Check for `<Data Center>/Mods/` again.

### MelonLoader Does Not Start

Check that the game folder contains:

```text
MelonLoader/
version.dll
```

On Windows, make sure antivirus software did not quarantine MelonLoader files.

On Linux / Proton, launch the game through Steam after installing MelonLoader.
For Steam Flatpak, confirm MelonLoader was installed into the Flatpak Steam
library path, not a different host Steam path.

### The Log Says No Support Module Loaded

Known Data Center / MelonLoader IL2CPP generation failures may show:

```text
BadImageFormatException: Duplicate type with name '<>O'
No Support Module Loaded!
```

Try this:

1. Close Data Center.
2. Update MelonLoader to the version recommended by this mod release.
3. Delete:

```text
<Data Center>/MelonLoader/Il2CppAssemblies/
```

4. Start Data Center again.
5. Let MelonLoader regenerate assemblies.
6. Check `Latest.log`.

If you are building from source, this repository includes an advanced repair
script for this specific generated assembly issue:

```bash
DATA_CENTER_GAME_ROOT="/path/to/Data Center" ./scripts/patch-unity-coremodule.sh
```

Most users should not need that script unless the maintainer asks for it.

### The Cart Menu Opens But Is Empty

An empty cart menu is normal.

Try this:

1. Pick up an item.
2. Press `E` on the cart to store it.
3. Open the cart menu again.

If you expected `Collect` to grab something, move the cart closer or increase
`BulkPickupRadiusMeters`, restart the game, and try again.

### Collect Does Not Grab A Bought Item

Try this:

1. Make sure the item has physically spawned in the world or storage container.
2. Open the storage container door if the item is hidden behind it.
3. Move the cart closer.
4. Open the cart menu and press `Collect` again.
5. Check `Latest.log` for a bulk-add message.

If it still fails, report the item name and where the item was: on the ground,
in storage, on the cart, or still in the shop.

### The Cart Collected Something It Should Not Have

If the item is trash, use the red `X` and confirm deletion.

If the item is not trash, click the row to take it out and put it somewhere
safe.

When reporting this bug, include:

- what item was collected;
- whether it was bought or unbought shop stock;
- whether it was on the ground, in storage, on the cart, or in a rack;
- the relevant `MelonLoader/Latest.log`.

### Drop Or Interact Prompts Look Wrong

If prompts are missing or duplicated after taking an item from the cart:

1. Restart Data Center.
2. Re-test with the latest mod build.
3. Include `Latest.log` if the problem repeats.

### Escape Opens The Pause Menu

The cart menu is intended to consume `Esc`. Pressing `Esc` while the cart menu
is open should close only the cart menu.

If the pause menu also opens:

1. Update the mod.
2. Restart Data Center.
3. Re-test with the cart menu open.
4. Include `Latest.log` if reporting the issue.

### Text Is Too Small Or The Menu Is Too Large

Edit:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

Useful settings:

```text
MenuWidthRatio
MenuHeightRatio
MenuMaximumWidth
ItemRowHeight
TitleFontSize
HeaderFontSize
ItemFontSize
SearchFontSize
ButtonFontSize
```

Restart Data Center after changing config.

### The Mod Fails After A Game Update

Game updates can change Unity IL2CPP metadata and break MelonLoader-generated
assemblies or mod patches.

Try this:

1. Close Data Center.
2. Update MelonLoader.
3. Delete `<Data Center>/MelonLoader/Il2CppAssemblies/`.
4. Launch Data Center and let MelonLoader regenerate assemblies.
5. Reinstall the latest version of this mod.

If it still fails, report the new `Latest.log`.

## Bug Reports

Useful bug reports include:

- operating system: Windows, Linux Steam, or Linux Steam Flatpak;
- Proton version, if on Linux;
- Data Center version, if Steam shows one;
- MelonLoader version;
- mod version;
- whether it happens in a new save or only an older save;
- exact steps to reproduce;
- the full `MelonLoader/Latest.log` from the failed session.

Do not paste only the last line of the log. The startup section usually matters.

## Uninstall

1. Close Data Center.
2. Delete these files from `<Data Center>/Mods/`:

```text
DataCenterBlackHoleCart.dll
DataCenterBlackHoleCart.deps.json
```

3. Start Data Center.

To remove the config too, delete:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

This does not uninstall MelonLoader.

## Build From Source

End users should install a release ZIP. Building from source is for developers.

Requirements:

- .NET SDK 6.0 or newer;
- Data Center installed;
- MelonLoader installed and launched once so generated IL2CPP assemblies exist.

Build:

```bash
dotnet build src/DataCenterBlackHoleCart/DataCenterBlackHoleCart.csproj -c Release \
  -p:DataCenterGameRoot="/path/to/Data Center"
```

Output:

```text
src/DataCenterBlackHoleCart/bin/Release/net6.0/DataCenterBlackHoleCart.dll
src/DataCenterBlackHoleCart/bin/Release/net6.0/DataCenterBlackHoleCart.deps.json
```

Copy those two files into `<Data Center>/Mods/`.
