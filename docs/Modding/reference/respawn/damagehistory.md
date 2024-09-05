# Damage History

After a player receives damage it is stored by the game in an array of
the following struct. The information in that struct is final and
changing it does not affect the game.

## DamageHistoryStruct

Getting the info from the entity
\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^\^

You can get the damage history for any player entity with
`player.e.recentDamageHistory`, this is of the type
`array<DamageHistoryStruct>` and gets automatically updated by the game.
The higher the index the older the `DamageHistoryStruct` is ( so to get
the most recent struct you do `player.e.recentDamageHistory[ 0 ]` ).

### Getter functions

> 
>
> param entity player
>
> :   The player you want the damage history from.
>
> param float time
>
> :   How old the damage history can be in seconds.
>
> returns
>
> :   All `DamageHistoryStruct` found in the given time frame.

### Setter functions

> Removes all `DamageHistoryStruct` in the time frame `time - maxTime`
>
> param entity player
>
> :   The player you want to update the damage history from.
>
> param float maxTime
>
> :   How old the damage history can maximally be
>
> param float time
>
> :   How old the damage history can be in seconds.

## Built in Checks

> !!! note
> !!! title
> Note
> :::
>
> > 
> ::::
