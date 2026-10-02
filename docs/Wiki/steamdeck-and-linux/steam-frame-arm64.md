# Steam Frame (ARM64)

!!! info
    This page covers running Northstar on **Steam Frame**, where SteamOS is `aarch64` and Windows
    games run through **Proton ARM64** (WoW64 + FEX). It is community-tested with the
    [CircuitLord Titanfall 2 VR mod](https://github.com/CircuitLord/CircuitLordVRModInstaller);
    the platform caveats below apply to Northstar generally.

Because the CPU is ARM64, x86-64 game code is emulated. This is the main difference from the
Steam Deck guide and is responsible for almost every quirk below.

## 1. Run vanilla Titanfall 2 once

Launch vanilla Titanfall 2 through Steam before installing anything. Steam installs and signs the
EA app in for you through its `steam2ea://launchgame/1237970` handoff, which is also how the game
authenticates later.

!!! warning
    If the EA app is not signed in, Northstar will start the EA app and then wait forever at its
    login screen (the EA app's embedded browser is unreliable under Proton). Always launch from
    Steam so the EA app gets signed in automatically.

## 2. Install the x86-64 MSVC runtime (required on ARM64)

On ARM64, an x86-64 process picks up the **Aarch64** `msvcp140.dll` / `vcruntime140.dll` from
`C:\windows\system32` and crashes (`EXCEPTION_ACCESS_VIOLATION`). Northstar and plugins use this
runtime, so the game will crash early without the x86-64 copies.

Put the **x86-64** versions next to `Titanfall2.exe`:

```
<Titanfall 2>/msvcp140.dll
<Titanfall 2>/vcruntime140.dll
<Titanfall 2>/vcruntime140_1.dll
```

X86-64 copies ship with the EA app:
`<compatdata>/1237970/pfx/drive_c/Program Files/Electronic Arts/EA Desktop/<version>/EA Desktop/`.

Platform bug reference: <https://github.com/ValveSoftware/Proton/issues/10211>

## 3. Install Northstar

Prefer a **manual install**: download the latest release from the
[Northstar releases page](https://github.com/R2Northstar/Northstar/releases) and extract it into
your Titanfall 2 folder, or use a third-party installer that runs on ARM64.

!!! note
    The GUI installers (FlightCore, Viper) are x86-64 desktop applications and may not run on
    Steam Frame without their own workarounds. Manual extraction is the most reliable route.

## 4. Launching Northstar

On Steam Deck the usual trick is adding `%command% -northstar` as a launch option. On Steam Frame
this does **not** work the same way, because Titanfall 2 is launched as the
`steam2ea://launchgame/1237970` handoff rather than `Titanfall2.exe` directly, and extra arguments
get appended to that URL.

Instead, run Northstar while keeping Steam's EA handoff:

1. Back up the real executable and install Northstar under the name Steam launches:
   ```sh
   GAME="$HOME/.local/share/Steam/steamapps/common/Titanfall2"
   cp -p "$GAME/Titanfall2.exe" "$GAME/Titanfall2_vanilla.exe"
   cp -f "$GAME/NorthstarLauncher.exe" "$GAME/Titanfall2.exe"
   ```
   (With a separate Northstar profile, e.g. the VR mod's `TF2VR`, also link it so it loads by
   default: `ln -sfn TF2VR "$GAME/R2Northstar"`.)
2. Add any engine arguments Northstar needs to `ns_startup_args.txt` in the game folder instead of
   a Steam launch option, for example:
   ```
   -novid -windowed -w 1280 -h 720
   ```
3. Launch Titanfall 2 from Steam (the normal Play button). Steam performs the EA sign-in, then
   launches your Northstar executable.

To return to vanilla, restore `Titanfall2_vanilla.exe` over `Titanfall2.exe` and remove any
profile symlink / `ns_startup_args.txt`.

## 5. Performance

Steam Frame's ARM64 SoC emulates x86-64, so CPU-bound games like Titanfall 2 are much more
demanding than on a Deck. Notes from testing:

- 90 Hz panel; native per-eye resolution is 2160×2160.
- Light scenes can hit the panel refresh; heavy combat can drop well below it.
- Watch CPU temperatures — sustained heavy load reaches 85-90 °C and the device throttles.
- `xalia.exe` (Wine's accessibility bridge) can consume a noticeable amount of CPU; it is spawned
  automatically.
- For OpenXR/VR apps the per-app render scale in
  `~/.config/openvr/config/steamvr.vrsettings` controls resolution, e.g.:
  ```json
  "steam.app.1237970" : { "supersampleScale" : 0.6 }
  ```
  (a global `"steamvr"` `"supersampleManualOverride": true` may be required for it to apply).
- **Foveated rendering is not implemented yet** ([CircuitLord#15](https://github.com/CircuitLord/CircuitLordVRModInstaller/issues/15)).
  Titanfall 2 VR is GPU-bound in combat on Steam Frame, and the headset has eye tracking, so
  dynamic foveation (or even fixed foveation) would help standalone hardware significantly. Until
  then, expect heavy fights to drop well below the panel refresh.

## Troubleshooting

- Check `Titanfall2.log`-style output in the Northstar console, and plugin logs under the profile.
- If the game crashes immediately, confirm the three x86-64 MSVC runtime DLLs above are present.
- If the EA app sits on a login screen, launch vanilla Titanfall 2 through Steam once first.
