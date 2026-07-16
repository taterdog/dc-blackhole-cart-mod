# Data Center Black-Hole Cart

This is the public download and installation repository for **Data Center
Black-Hole Cart**, a MelonLoader mod for the Steam game **Data Center**.

The mod turns the in-game cart into a searchable inventory.

## What You Can Do

- Hold an item and press `E` on the cart to store it.
- Press `E` on the cart with empty hands to open the cart menu.
- Click an item in the menu to put it back in your hands.
- Use `Collect` to pull eligible nearby ground, cart, storage, and purchased
  shop items into the cart and clean up empty SFP/QSFP boxes.
- Search, sort, scroll, and delete stored cart items.
- Change cart part colors with hex color codes in the config file.
- Keep each cart inventory inside its matching Data Center save so Steam Cloud
  carries the cart and world together between Windows and Linux/Proton.
- Automatically repair the known malformed MelonLoader-generated CoreModule
  before the cart mod loads.

## Download

Current release: `v0.2.0`.

Download the ready-to-install ZIP:

[releases/DataCenterBlackHoleCart-v0.2.0.zip](releases/DataCenterBlackHoleCart-v0.2.0.zip)

ZIP SHA-256:

```text
54b91c07d22737763d4963cbd04fa54acfda4fa5662c1467a71b10dd5b30cb09
```

The ZIP has the complete install layout:

```text
Mods/
  DataCenterBlackHoleCart.dll
  DataCenterBlackHoleCart.deps.json
Plugins/
  DataCenterBlackHoleCart.Bootstrap.dll
  DataCenterBlackHoleCart.Bootstrap.deps.json
README.txt
```

Both `Mods/` and `Plugins/` are required. Merge both folders into the Data
Center game folder; keep the bootstrap under `Plugins/`.

## What's New In v0.2.0

- Cart inventory is now embedded in Data Center's normal save instead of using
  machine-local JSON as its primary storage.
- Steam Cloud can carry the saved cart between Windows and Linux/Proton with
  the matching world save.
- Existing `0.1.x` cart JSON can be imported once when a save does not yet have
  an embedded cart record.
- A required early-start bootstrap automatically repairs the known duplicate
  `<>O` metadata failure in generated `UnityEngine.CoreModule.dll` files.
- The release now uses ready-to-merge `Mods/` and `Plugins/` folders.

## Quick Install

1. Close Data Center.
2. Install MelonLoader into the Data Center game folder.
3. Start Data Center once with MelonLoader installed.
4. Quit after the game reaches the main menu.
5. Open the release ZIP and merge both its `Mods/` and `Plugins/` folders into
   the Data Center game folder.
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
  Plugins/
    DataCenterBlackHoleCart.Bootstrap.dll
    DataCenterBlackHoleCart.Bootstrap.deps.json
  UserData/
```

## Upgrading From v0.1.x

Older versions stored cart inventory as machine-local JSON under:

```text
<Data Center>/UserData/DataCenterBlackHoleCart/Saves/
```

Install `v0.2.0` on the computer that has the old JSON, load its matching save,
and save the game once. That embeds the cart in the normal save so Steam Cloud
can carry it to another computer or operating system. Steam never uploaded the
old sidecar by itself.

Keep the old JSON until the migrated cart has been verified. The mod retains
it as recovery data rather than deleting it after import.

## Save Behavior

Cart changes are committed only when Data Center saves the game. If you add or
remove cart items and then quit or load another save without saving, those cart
changes are discarded with the other unsaved world changes.

The cart record is part of the normal Data Center save. Backing up that save
also backs up its v0.2.0 cart inventory. The config file remains machine-local.

Before installing any mod on an important save, make a normal game-save
backup.

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

Look for lines that include:

```text
Data Center Black-Hole Cart Bootstrap
Support Module Loaded
Melon Assembly loaded: '.\Mods\DataCenterBlackHoleCart.dll'
Data Center Black-Hole Cart loaded.
Black-hole cart config loaded:
```

You can also test in game by walking to the cart with empty hands and pressing
`E`. The menu can open even when the cart is empty.

## Config Location

After first launch, the mod creates:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

Close Data Center before editing the file. Restart the game after saving
changes. Settings include the `Collect` radius, default name sort direction,
cart part colors, menu size, row height, and font sizes.

## CoreModule Recovery

The `Plugins/DataCenterBlackHoleCart.Bootstrap.dll` file automatically repairs
the known generated CoreModule defect during a normal game launch. No manual
repair script is included in the player package.

If `Latest.log` reports `Duplicate type with name '<>O'` or `No Support Module
Loaded!`:

1. Close Data Center.
2. Reinstall both the release `Mods/` and `Plugins/` folders.
3. Delete `<Data Center>/MelonLoader/Il2CppAssemblies/`.
4. Start Data Center through Steam and let MelonLoader regenerate its files.
5. Check `Latest.log` again.

## Repo Layout

```text
README.md
releases/
  DataCenterBlackHoleCart-v0.2.0.zip
```

## Uninstall

Take important items out of the black-hole cart and save the game before
uninstalling. Without the mod, embedded cart items are not available through
normal gameplay.

Close Data Center, then delete:

```text
<Data Center>/Mods/DataCenterBlackHoleCart.dll
<Data Center>/Mods/DataCenterBlackHoleCart.deps.json
<Data Center>/Plugins/DataCenterBlackHoleCart.Bootstrap.dll
<Data Center>/Plugins/DataCenterBlackHoleCart.Bootstrap.deps.json
```

To remove the machine-local config too, delete:

```text
<Data Center>/UserData/DataCenterBlackHoleCart.cfg
```

Uninstalling does not remove the embedded record from an existing Data Center
save. Legacy `0.1.x` JSON can be deleted separately after migration is verified
and it is no longer needed as recovery data.
