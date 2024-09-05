# Custom Northstar Callbacks

Callbacks added by Northstar

Callbacks within squirrel trigger functions when certain events occur.

They will also often pass arguments to those functions based on the
callbacks used.

## List of callbacks

Please refer to Respawn `../respawn/callbacks`  for the list of callbacks defined in respawn code.

### \_codecallbacks_common.gnut:

### \_custom_codecallbacks.gnut:

### \_items.nut:

### \_loadouts_mp.gnut:

### \_menu_callbacks.gnut:

### sh_remote_functions_mp_custom.gnut:

evac\\\_evac.gnut: \^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

gamemodes\\\_gamemode_fra.nut:
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

gamemodes\\sh_gamemodes_custom.gnut:
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

lobby\\\_lobby.gnut: \^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

lobby\\\_private_lobby.gnut:
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

melee\\sh_melee.gnut: \^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

> This callback gets triggered after the melee button is pressed to
> check if the action to execute the target is still valid. If one of
> the added callbacks return false the target won\'t be executed and
> will just be meleed.
>
> !!! note
>
> The execution prompt still pops up.
> ::::

mp\\\_ai_mp.gnut: \^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

mp\\\_base_gametype_mp.gnut:
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

mp\\\_gamestate_mp.nut: \^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

ui\\ui_mouse_capture.nut:
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^
