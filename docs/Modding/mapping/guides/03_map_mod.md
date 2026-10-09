# Custom Maps Mod

## Previously...
Read this guide once you have **compiled** your [first map](./guides/02_first_map)


## Which files to copy
After compiling, `remap`[^remap] should have created `.bsp` & `.ent` files.
These will be in the same folder as your `.map`.

[^remap]: MRVN-Radiant's `.map` compiler


## Where to copy them to
To load your map into Northstar we will need create a mod to "mount" the files

> TODO: link to other basic mod guides


## A basic custom maps mod

> TODO: screenshots

To get started, all you need is:

```
author.mod_name/
|-- mod.json   # mod description
|-- mod/maps/  # your files go here
```

Make the `author.mod_name` folder in `Titanfall 2/R2Northstar/mods`.[^moddir]
(You can substitute any name you want, it's just a template).

[^moddir]: where your other mods are installed

Then, copy the `.bsp` & `.ent` files from earlier into `author.mod_name/mod/maps/`

### Example `mod.json`

```json
{
    "Name": "author.mod_name",
    "Description": "my first map",
    "Version": "0.1.0",
    "LoadPriority": 0,
    "RequiredOnClient": true
}
```


## Playing your map

Once you've made the mod folder, fire up Northstar & it should load the mod autoamtically

> TODO: screenshot confirming the mod is loaded in the Mods menu

Go into multiplayer so we can fire up a custom server

> [!NOTE]
> Your map will not appear on the custom server map list.
> Don't worry! That's normal.

> TODO: hint at extending the map list in a future guide
> (or request a Northstar feature / mod which adds a custom maps menu)

You'll need to fire up the `developer console`, do this by pressing the tilde (`~`) key
(up and left from `1` on most keyboards)

> TODO: do users need to enable dev console, or does Northstar have it on by default?

Type in `map mp_myfirstmap` & hit enter to start a match of skirmish on your map

> TODO: setting gamemode before launching
> TODO: troubleshooting (no valid spawns etc.)

> [!TIP]
> You can quit out of Northstar fast by typing `exit` in console


## Next Time...
[Using Assets](./guides/04_rpak_assets)
