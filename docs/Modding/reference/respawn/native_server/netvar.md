# Networked Data

## Networked Variables

> Registers a named networked variable.

> Gets the internal index used to reference a scripted network variable.
> For use with `FX_PATTACH_SCRIPT_NETWORK_VAR`.

## Remote Functions

Remote functions allow the `SERVER` to call registered script functions
on the `CLIENT` and `UI` VM.

> Begin registration of remote functions.

> Finish registration of remote functions.

> !!! note
> !!! title
> Note
> :::
>
> This function is not native. It\'s defined in
> [Northstar.CustomServers](https://github.com/R2Northstar/NorthstarMods/blob/main/Northstar.CustomServers/mod/scripts/vscripts/sh_remote_functions_mp_custom.gnut)
> ::::
>
> Registers a callback when Remote functions are being registered.
>
> To register custom remote functions you are **required** to use this
> callback because functions can only be registered once.
>
> ``` 
> globalize_all_functions
>
> void function MyMod_Init()
> {
>   AddCallback_OnRegisteringCustomNetworkVars( MyModRegisterRemoteFunctions )
> }
>
> void function MyModRegisterRemoteFunctions()
> {
>   Remote_RegisterFunction( "ExampleRemoteFunction" )
> }
>
> void function ExampleRemoteFunction() {}
> ```

> Register a function name to be used in remote calls.

> !!! note
> !!! title
> Note
> :::
>
> Allowed extra parameter types are null, bool, int, and float.
> ::::
>
> Given a player, function name, and optional parameters, call function
> in client script.
>
> Then call it again if we rewind and play a kill replay. The command
> will not reach the client at all if called during a span of time the
> player skips because they were watching a replay.

> !!! note
> !!! title
> Note
> :::
>
> Allowed extra parameter types are null, bool, int, and float.
> ::::
>
> Given a player, function name, and optional parameters, call function
> in client script.
>
> Does not get called again in replays.

> !!! note
> !!! title
> Note
> :::
>
> Allowed extra parameter types are null, bool, int, and float.
> ::::
>
> Given a player, function name and optional parameters, call function
> in UI script.

## Replays

While not being networked themselves, these are used by remote
functions.
