# Using Assets

## Previously...
You don't need to do this one, we're still figuring out the process.
> TODO: redirect to a guide on including basic `.vmt` materials


## Why `.rpak`
Most materials in Titanfall 2 are stored in `.rpak`.
Titanfall 1 used the older Source Engine system of `.vmt` & `.vtf` files in `.vpk` archives.
A small handful of `.vmt` materials remain in Titanfall 2.
However, they aren't the best for a finished map.

Only `.rpak` materials can receive light & shadow
(though MRVN maps can't leverage this much just yet)


## `.rpak` Aliasing

You can borrow assets from another map by aliasing it's `.rpak`:

```
author.mod_name/
|-- mod.json
|-- mod/maps/
|-- paks/rpak.json
```

### Example `rpak.json`

```json
{
    "Aliases": {
      "mp_myfirstmap.rpak": "sp_crashsite.rpak"
    }
}
```

> [!WARNING]
> This `rpak.json` format might be deprecated.
<!-- see PR 7-->


## RSX

### Extract Asset List
> TODO

### Extract `matl` & `txtr`
> TODO


## MRVN
> TODO:
> writing a `.shader` from an RSX asset list.
> using `_col` textures as thumbnails.
> transparency & compile flags (advanced)

> TODO: automate all this so users don't have to write `.shader` files
> ideally a `.vmt` equivalent for each material.
> the dream is to have a material format that can be fed to RePak.
