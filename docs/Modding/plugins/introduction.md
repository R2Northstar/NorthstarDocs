# Introduction

!!! note

    Writing plugins require some very basic familiarity with C++

Plugins differ to script mods in that they are dynamically linked, precompiled modules. Only install a plugin if you trust the source you downloaded it from.

## Installation

Any `.dll` file located in the directories `<Northstar Profile>/plugins/` and `<Northstar Profile>/packages/<Thunderstore package>/plugins/` will be attempted to load as a plugin.

To manually install a plugin, copy the plugin `.dll` into the `<Northstar Profile>/plugins/` directory.

!!! note

    The default northstar profile name is `R2Northstar`. Profiles are located in the same location as `NorthstarLauncher.exe`.


Any Plugin is only valid if it exposes every required [interface](interfaces.md).

If a plugin does not expose every Interface the Launcher requires, it is unloaded immediately.

## Development

To debug a plugin it's recommended to compile Northstar itself or download the debug data from the [Release Page](https://github.com/R2Northstar/NorthstarLauncher/releases).

When developing a plugin it's usually easier to output the binary directly in the `<profile>/plugins/` directory, the `packages/` directory is usually only used for complete packaged mods downloaded from Thunderstore.

### Valid plugins

Every plugin must fulfill these criteria to be considered valid by Northstar.

Invalid plugins get unloaded as soon as possible.

- The plugin module must export a function named [`CreateInterface`](interfaces.md/#CreateInterface) that returns an interface instance when called.

- Every [required interface](required-interfaces.md) must be exposed via `CreateInterface`

### Debugging

If you know how to use a debugger you can safely skip this.

For simplicity it's assumed your development environment is Visual Studio and you're compiling Northstar from source.

Otherwise are the steps basically the same everywhere else.

1) Clone the [Launcher](https://github.com/R2Northstar/NorthstarLauncher)

2) Set the binary output directory to the location wherever you have installed your game. The compiled `NorthstarLauncher.exe` should be outputted next to `Titanfall.exe`.

3) Launch `NorthstarLauncher.exe` with a debugger or attach a debugger to a running process

4) Load debug symbols of your plugin(s) (`myplugin.pdb`) in the debugger

That's it.

### Hooks

Any Plugin can install hooks anywhere in memory it desires. However, plugins should avoid hooks if possible because of conflicts with Northstar itself or hooks installed by other plugins.

It is not generically possible to determine if a given address has already been hooked by a different plugin and there is currently **no mechanism for plugins to share information which addresses have hooks installed**.

Northstar does not expose an interface to (un)install hooks. Every plugin is expected to use their own provider.

## Examples and Libraries

- A small plugin [""framework""](https://github.com/uniboi/NSPluginTemplate/) to show the basics of writing plugins and Squirrel bindings in C

- A complete [rust plugin library](https://crates.io/crates/rrplug) that allows you to easily integrate safely with large parts of the engine itself