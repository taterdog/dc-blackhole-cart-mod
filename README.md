# Data Center Black-Hole Cart

This is the public download and installation repo for **Data Center
Black-Hole Cart**, a MelonLoader mod for the Steam game **Data Center**.

The mod turns the in-game cart into a searchable inventory.

## What You Can Do

- Hold an item and press `E` on the cart to store it.
- Press `E` on the cart with empty hands to open the cart menu.
- Click an item in the menu to put it back in your hands.
- Use `Collect` to pull eligible nearby ground, cart, storage, and purchased
  shop items into the cart.
- Search, sort, scroll, and delete stored cart items.
- Change cart part colors with hex color codes in the config file.
- Cart contents persist per Data Center save file.

## Download

Current release: `v0.1.13`.

Download the ready-to-install ZIP:

[releases/DataCenterBlackHoleCart-v0.1.13.zip](releases/DataCenterBlackHoleCart-v0.1.13.zip)

Only those two files go into the game's `Mods` folder.

## Quick Install

1. Close Data Center.
2. Install MelonLoader into the Data Center game folder.
3. Start Data Center once with MelonLoader installed.
4. Quit after the game reaches the main menu.
5. Copy these two files into `<Data Center>/Mods/`:

```text
DataCenterBlackHoleCart.dll
DataCenterBlackHoleCart.deps.json
```

6. Start Data Center through Steam.
7. Load a save, walk to the cart with empty hands, and press `E`.

If the cart menu opens, the mod is installed.

The final layout should look like this:

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

## Requirements

- Steam copy of **Data Center**.
- MelonLoader installed into the Data Center game folder.
- MelonLoader `0.7.3` or newer, unless a release note says otherwise.
- .NET 6 runtime if MelonLoader does not provide it automatically.

Useful links:

- MelonLoader releases: <https://github.com/LavaGang/MelonLoader/releases>
- MelonLoader wiki: <https://melonwiki.xyz/>
- .NET 6 downloads: <https://dotnet.microsoft.com/en-us/download/dotnet/6.0>
- .NET Linux install docs: <https://learn.microsoft.com/en-us/dotnet/core/install/linux>

## Confirm The Mod Loaded

Open:

```text
<Data Center>/MelonLoader/Latest.log
```

Look for:

```text
Melon Assembly loaded: '.\Mods\DataCenterBlackHoleCart.dll'
Data Center Black-Hole Cart loaded.
Black-hole cart config loaded:
Support Module Loaded
```

You can also test in game by walking to the cart with empty hands and
pressing `E`.

## Config Location

After first launch, the mod creates:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

Close Data Center before editing the file. Restart the game after saving
changes.

## Persistent Cart Files

The mod stores per-save cart inventory files here:

```text
<Data Center>/UserData/DataCenterBlackHoleCart/Saves/
```

If you back up a game save and want the black-hole cart contents too, back up
this folder along with the game's normal save data.

## Repo Layout

```text
README.md
releases/
  DataCenterBlackHoleCart-v0.1.13.zip
```

## Uninstall

Close Data Center, then delete these files from `<Data Center>/Mods/`:

```text
DataCenterBlackHoleCart.dll
DataCenterBlackHoleCart.deps.json
```

To remove the config too, delete:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

To remove persisted black-hole cart inventories too, delete:

```text
<Data Center>/UserData/DataCenterBlackHoleCart/
```
