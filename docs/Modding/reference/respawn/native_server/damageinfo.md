# DamageInfo

DamageInfos are variables holding information about damage inflicted on
an entity.

Because damageInfo instances are implemented as userdata they can\'t be
typed.

## Getters

> Returns the attacker of this damageInfo

> Returns the inflictor of this damageInfo

> Returns the weapon that dealt this damage

> Get if this damage is supposed to kill the victim regardless of health

> Get the inflicted damage

> Returns the position where the damage originated. Usually this is the
> barrel attachment of the weapon that inflicted the damage.

# DamageInfo-GetDamageType

# damage-source-id-overview

> Returns the `eDamageSourceId`
>
> `damageSourceId` is an `int` that references an `enum` and can be used
> to identify what source damage came from.
>
> `damageSourceId` is mostly found as an argument in some kill and
> damage related functions. Respawn has created a function that will
> attempt to localise the damageSourceId inputed. To add your own custom
> `damageSourceID` , see:
> `../../northstar/customdamagesources` 
>
> Other useful functions can be found in the `damageinfo` section of
> this page and in `entities` 
>
> `GetObitFromdamageSourceId` is a global function that attempts to
> localise the `damageSourceId` inputed, if it cannot get a localised
> string it will simply return the localisation string of the source.

> Get the distance from where the bullet/projectile was fired.

> If it\'s a radius damage, gives the distance from the center of the
> blast. Otherwise defaults to zero.

> Get damage force vector.

> Checks if code is allowing this entity to ragdoll on death

> Get all () flags. *damageflag used to be here*

> \"Returns true if contains all given () flags. *and here too*

> Returns weapon name, even if weapon entity is gone

> Returns if stats should be recorded for damage weapon

## Setters

> Sets whether this damage should force a kill

> Set the amount of damage

> Overrides the damage type that was set by script when firing the
> weapon.

> Add a damage flag.

> Remove damage flag.

> Sets the damage source identifier.

> Set what death (anim) package to use if this damage kills the guy.

> Set damage force vector

> Set which direction the target should flinch in.

> Add a () flag. *here aswell*

## Utils

TODO: fix helpers section, its been removed for redundancy

## Damage Flags {#damage-flag-overview}

You can get a bitflag of all damage types used with
`DamageInfo_GetDamageType <DamageInfo-GetDamageType>`.

dropdown 
!!! info[TODO]
Turn this into a real dropdown
:::
Damage flags


List of all Damage flags

  Variable name           Value
  ----------------------- -------
  DF_GIB                  1
  DF_DISSOLVE             2
  DF_INSTANT              3
  DF_NO_SELF_DAMAGE       4
  DF_IMPACT               5
  DF_BYPASS_SHIELD        6
  DF_RAGDOLL              7
  DF_TITAN_STEP           8
  DF_RADIUS_DAMAGE        9
  DF_ELECTRICAL           10
  DF_BULLET               11
  DF_EXPLOSION            12
  DF_MELEE                13
  DF_NO_INDICATOR         14
  DF_KNOCK_BACK           15
  DF_STOPS_TITAN_REGEN    16
  DF_DISMEMBERMENT        17
  DF_MAX_RANGE            18
  DF_SHIELD_DAMAGE        19
  DF_CRITICAL             20
  DF_SKIP_DAMAGE_PROT     21
  DF_HEADSHOT             22
  DF_VORTEX_REFIRE        23
  DF_RODEO                24
  DF_BURN_CARD_WEAPON     25
  DF_KILLSHOT             26
  DF_SHOTGUN              27
  DF_SKIPS_DOOMED_STATE   28
  DF_DOOMED_HEALTH_LOSS   29
  DF_DOOM_PROTECTED       30
  DF_DOOM_FATALITY        31
  DF_NO_HITBEEP           32
:::

!!! dropdown
Damage types

``` 
global enum damageTypes
{
    gibs = (DF_GIB)
    largeCaliberExp  = (DF_BULLET | DF_GIB | DF_EXPLOSION)
    gibBullet = (DF_BULLET | DF_GIB)
    instant = (DF_INSTANT)
    dissolve = (DF_DISSOLVE)
    projectileImpact = (DF_GIB)
    pinkMist = (DF_GIB) //If updated from DF_GIB, change the DF_GIB in Arc Cannon to match.
    ragdoll = (DF_RAGDOLL)
    titanStepCrush = (DF_TITAN_STEP)
    arcCannon = (DF_DISSOLVE | DF_GIB | DF_ELECTRICAL )
    electric = (DF_ELECTRICAL) //Only increases Vortex Shield decay for bullet weapons atm.
    explosive = (DF_RAGDOLL | DF_EXPLOSION )
    bullet = (DF_BULLET)
    largeCaliber = (DF_BULLET | DF_KNOCK_BACK)
    shotgun = (DF_BULLET | DF_GIB | DF_SHOTGUN )
    titanMelee = (DF_MELEE | DF_RAGDOLL)
    titanBerserkerMelee = (DF_MELEE | DF_RAGDOLL)
    titanEjectExplosion = (DF_GIB | DF_EXPLOSION)
    dissolveForce = (DF_DISSOLVE | DF_KNOCK_BACK | DF_EXPLOSION)
    rodeoBatteryRemoval = (DF_RODEO | DF_EXPLOSION | DF_STOPS_TITAN_REGEN )
}
```

