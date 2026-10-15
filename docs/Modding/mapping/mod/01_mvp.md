# Basic Map Mod

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


## Next Time...
[Playing Your Map](./02_load_map.md)
