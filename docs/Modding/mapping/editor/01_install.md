# Installing MRVN-Radiant

## Getting the latest build

<!-- TODO: MRVN-Radiant GitHub Releases -->

### Discord
If you're in the Northstar Discord, there's a copy of MRVN in `#maps-chat` pins

<img
  src="/_static/mapping/MRVN_download_Discord.webp"
  alt="Northstar Discord maps-chat pins"
/>

!!! warning
    The current pinned version is extremely outdated (from 2024!)

### GitHub Actions
Alternatively, download from [GitHub Actions](https://github.com/MRVN-Radiant/MRVN-Radiant/actions)

<img
  src="/_static/mapping/MRVN_download_GitHub.webp"
  alt="GitHub Actions download page for MRVN-Radiant"
/>

!!! note
    Download links may not be available if you aren't logged in or the build is too old


## Unzip & Run
Extract the whole `.zip` to a folder

!!! warning
    Contents are loose

Run `radiant.exe` (just `radiant` for Linux users)

> TODO: can't actually replicate this on my machine (LMDE 7): "missing shared libraries"


## Setting up folders
When MRVN first starts up you will be presented with a splash screen:

<img
  src="/_static/mapping/MRVN_splash.webp"
  alt="MRVN-Radiant's Splash Screen dialog"
/>

!!! note
    The first time you start up MRVN will ask for an engine path.
    Further down we'll explain how to change this path.

Once you get past the splash screen, you'll be greeted with a new, empty map:

<img
  src="/_static/mapping/MRVN_new_map.webp"
  alt="any empty map in MRVN-Radiant"
/>

Now we're going to set the engine path, go into `Edit > Preferences`:

<img
  src="/_static/mapping/MRVN_edit_preferences.webp"
  alt="MRVN-Radiant's Edit menu, with Preferences selected"
/>

Select the `Game > Paths` tab on the left to reach this menu:

<img
  src="/_static/mapping/MRVN_engine_path.webp"
  alt="The Game Paths tab in MRVN's Preferences menu, cursor hovering over Engine Path"
/>

Click on the file icon for `Engine Path` to open a file browser.
From here you'll pick a folder to keep you project files in.

!!! note
    `Engine Path` will create subfolders for each game MRVN-Radiant supports.
    But MRVN should only create them when you pick a different game on startup.

Your `Engine Path` will contain these folders:

<img
  src="/_static/mapping/engine_path_contents.webp"
  alt="A file browser open on 'MRVN-Radiant_games/', it contains 'Titanfall2/'"
/>

### Game Folder layout
```
Titanfall2/
|-- maps/
|-- models/
|-- shaders/
|-- textures/
```

Inside each game folder MRVN will create a `maps/` folder.
Whenever you open or save a map, MRVN will open a file browser here.

All the other folders will contain assets for **MRVN**.
The formats & requirements are different to Northstar.

!!! tip
    You can download some assets to get started from [MRVN-Resource-Pack](https://github.com/MRVN-Radiant/MRVN-Resource-Pack/releases/latest)


## Next Time...
Learn about basic [Mapping Concepts](./02_concepts.md).
