# Useful Functions

## Custom Ejection Messages

### How ejection messages are chosen

When ejecting the game selects a random number between 0 and 1, if this
number is greater than 0.15 then a random common eject message is
returned, if it is less than 0.15 then a rare ejection message is
returned.

### Adding new messages

Using `AddCommonEjectMessage( String message )` and
`AddRareEjectMessage( String message )` in script additional messages
can be added to the pool of potential ejection messages

### Localisation

Like most things custom ejection messages can be localised through
keyvalues

There are no functions to remove ejection messages, however existing
ones can be altered by modifying localisation files

Below are a list of useful functions added by Northstar.

## Player functions

### Check for different weapon types on a player

### Get weapon from entity

Take weapon from Entity \~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

Validity checks for player
\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

> !!! note
> !!! title
> Note
> :::
>
> Respawn comment next to the function:
>
> `TODO: This is a copy of SP's PlayerPosInSolid(). Not changing it to avoid patching SP. Merge into one function next game`
> ::::

> !!! note
> !!! title
> Note
> :::
>
> Respawn comment next to the function:
>
> `TODO:  This function returns true for a player standing inside a friendly grunt. It also returns true if you are right up against a ceiling.Needs fixing for next game`
> ::::

### Change a players invincibility

## Entity functions

### Turret functions

### Rest so far to be sorted

> !!! note
> !!! title
> Note
> :::
>
> this function only exists on clients
> ::::

> !!! note
> !!! title
> Note
> :::
>
> A cleaner way to get a player:
> ::::

> !!! note
> !!! title
> Note
> :::
>
> this function only works on NPCs and not on players
> ::::

### Titans

## Gamemode functions

> !!! note
> !!! title
> Note
> :::
>
> Does not work for FFA modes
> ::::

> Returns the local player\'s UID, else `null`. Available on CLIENT, UI
> and SERVER VM.

## Threaded conditonals

## Random functions

## Type Utilities

### Table

### Arrays

> !!! warning
> !!! title
> Warning
> :::
>
> this returns `-1` if the item was not found in the array
> ::::

> Removes a variable by value instead of index.

> Reorders the array randomly.

> returns a random element from array

> changes the size of the array to the first int, new slots will be
> filled with the 2nd argument.

!!! note
!!! title
Note
:::

A few built-in functions you can give as arguments to sort an array.

!!! dropdown
Array Sort Functions

Functions for score comparison
:::
:::::

> !!! note
> !!! title
> Note
> :::
>
> Returns a section of the array as new array. Copies from start to the
> end (not included). If start is negative the index is calculated as
> length + start, if end is negative the index is calculated as length +
> end. If end is omitted end is equal to the array length.
> ::::

### String

> returns a unique string

> !!! note
> !!! title
> Note
> :::
>
> returns the new string with the first occurance of the toReplace
> string.
> ::::

> Returns a formatted template

> !!! warning
> !!! title
> Warning
> :::
>
> returns `null` if the string is not found.
>
> You can eliminate the possibility of the returned index being null by
> casting like this:
>
> ``` 
> int ornull index = GetMapName().find( "mp" )
>
> if( !index )
>     return
> int( index )
> int n = index + 1 //now we do not need the ornull anymore
> ```
> ::::

### Float

### Integer

### Vectors
