# Singleplayer

## SaveGames

> Do a save.

> Do a save.
>
> Will call back `bool CodeCallback_SaveGameIsSafeToCommit()` to
> validate if it is ok to commit the save file.

> If there is an outstanding save commit, accept it asap.

> If there is an outstanding save commit, reject it asap.

> Do a restore.

> Checks if a file is ok to use.

> Return the script version of a save load.

> Return the script start point of a save load.

> Return the map name of a save load.

## Level Loading

> Loads a new level. The data in `transitionStruct` can be read in the
> next level with `GetLevelTransitionStruct()`.

> Reads the transition data set by `ChangeLevel()` on the previous map.
> Return `null` if this is the first map or the previous map didn\'t
> supply any data.

## Timeshift

## BT Loadouts
