# Entities

There are different Classes for Server and Client. Classes that start
with `C_` are exclusive to the Client VM and classes that only have the
`C` Prefix are only usable in the Server VM.

Most entries have three sub entries: The class available to the SERVER,
the CLIENT and methods that are available on both VMs.

For a graphic reprasentation of the Server and Client class inheritance,
refer to [this chart](http://salzgrube.club/class_graph_dynamic.html)

!!! note

Pay attention to the `extends` keyword for each class! You can use every
property of that the parent class has access to!

This List of Classes and their Methods is incomplete!
::::

## CBaseEntity / C_BaseEntity

Basic entity that most other entities inherit from.

### Shared

> > Hides the ent. (invisible)
>
> > Shows the ent. (visible)
>
> > Destroys this entity.
>
> > `../../native/async` 
> >
> > Signals on this entity
>
> > Ends this thread when the identifier is signaled on this entity
>
> > Halts this thread until a signal is activated for this entity
>
> > Executes the callback function when the signal is fired.
>
> > Disconnects the callback from the signal.
>
> > Connects an output on this entity to an input on another entity via
> > code. The `target` can be a name or a named entity.
>
> > Returns the Coordinates of this entity
>
> > Returns the direction this entity is facing to
>
> > Returns the position of this entities eyes
>
> > Returns the owner of this entity. Set the owner with `SetOwner`
>
> > Internal class name of the parent class. May return the identifier
> > name for some classes
>
> > Returns `true` if this entity is an NPC
>
> > Returns `true` if this entity is a Titan
>
> > Returns true if this entity is a gameplay-wise a human.
> >
> > For example, returns `true` if the entity is a grunt but `false` if
> > the entity is a Titan or spectre etc.
> >
> > However, players will always be Human, even when they are spectating
> > or their playermodel is robotic (for example when playing as stim)
>
> > Returns `true` if this entity is mechanical. Examples are Titans and
> > spectres
> >
> > !!! note
> >
> > This returns `true` for players that are playing mechanical classes
> > ::::
>
> > Returns `true` if this entity is currently phase shifting
>
> > Returns `true` if this entity is a player
>
> > Returns `true` if this entity is a projectile
>
> > Returns the asset this entity is being rendered with
>
> > Binds this entity to the parent. The child inherits the position and
> > rotation of the parent
>
> > Make this entity independent from its parent
>
> > Returns this entities parent
>
> > Set the model of this entity.
>
> > Similar to `SetValueForModelKey` but for FX.
>
> > Returns `0` for light armor and `1` for heavy armor
> >
> > Titans use heavy armor while pilots and similar use light armor
>
> > Returns the max health of this entity
>
> > Returns the current health
>
> > Returns the current shield health
>
> > Returns the maximum shield health of this entity
>
> > Returns `true` if this entity has gib models
>
> > Set the position of this entity
>
> > Returns the team of this entity
>
> > Returns the rotation of this entity
>
> > Set the rotation of this entity
>
> > The same as `GetValueForKey`
>
> > The same as `SetValueForKey`
>
> > Returns the velocity of this entity
>
> > Kill this entity: this function is deprecated because it has a
> > one-frame delay; instead, call ent.Destroy()
>
> > returns `true` if this entity is invulnerable
>
> > Returns the index of this entity
>
> > Set the team for this entity
> >
> > Skins based on team do not get updated. Use [SetSkin]
> > for this
>
> > Returns `true` if this entity is cloaked
>
> > Returns `true` if this entity is alive
>
> > Returns `true` if this entity is Valid.
> >
> > `IsValid( ent )` is a good alternative
>
> > Returns a normalized vector pointing forwards away from this entity.
>
> > Returns a normalized vector pointing to the right of this entity.
>
> > Returns a normalized vector pointing upwards from this entity.
>
> > Depends on the class.
> >
> > Returns a new instance of a class.
> >
> > You can invoke the constructor with brackets as well, for example
> > like this: `CBaseEntity()`
>
> > Allow or disallow this entity to cloak itself
>
> > Returns `true` if this entity can\'t be critted.
>
> > Returns `true` if this entity is a hologram
>
> > Returns `true` if this entity is touching the ground
>
> > Set the model this entity is being rendered with
>
> > Returns the script name of this entity.
>
> > Set the script name of this entity.
>
> > Returns `true` if this entity is breakable glass
>
> > Returns `true`\`if this entity is the gameworld
>
> > Returns `true` if this entity is a decoy
>
> > `DAMAGE_NO`, `DAMAGE_YES`, `DAMAGE_EVENTS_ONLY`
>
> > Set if this entity takes crit damage.
>
> > Set the velocity of this entity.
>
> > Always render this entity
>
> > Disable always rendering this entity
>
> > Sets the distance between a player and the entity at which the ent
> > will begin to fade out.
>
> > Disable all physics for this entity

### CBaseEntity

> > Set current health of this entity
>
> > Set max health of this entity
>
> > Set the owner of this entity
>
> > Kill this entity in the game sense - all callbacks and signals get
> > triggered
>
> > Returns `false` if this entity is solid
>
> > Moves this entity to `pos` over the duration of `moveTime` with ease
> > in and ease out
> >
> > !!! note
> > Entites that are not movers get teleported instantly
> > ::::
>
> > Rotate to the specified angles over time with ease in and ease out.
>
> > Make this entity vulnerable again
>
> > Make this entity invulnerable
>
> > Trigger AI now
>
> > Make this entity usable
>
> > Make this entity usable only for a specific group
>
> > Set the radius in which this entity can be interacted with
>
> > Make this entity unusable
>
> > Make this entity solid
>
> > Fire an output on this entity, with optional parm and delay
>
> > Fire an output on this entity, with optional parm and delay
> > (synchronous)
>
> > Trigger cloak flicker effect
>
> > Make this entity invisible
>
> > Make this entity visible
>
> > Set if this entity can be attacked by AI
>
> > Remove boss player reference from this entity.
>
> > Prints ent index, classname and target name of this entity to the
> > console.
>
> > \"consider this the mega hide\"
>
> > \"it\'s back!\"
>
> > this is a general purpose function that returns a string which, when
> > executed, runs the given function on this entity.
> >
> > the function must be called (or the entity deleted) at some point to
> > avoid leaking the new slot we make in this Table.
> >
> > compile with output with `compilestring`

### C_BaseEntity

> > Kill this client side prop.
>
> > Starts the highlight with the set configuration
>
> > Returns the EHandle of this entity.
>
> > Hide HUD elements
>
> > Show HUD elements
>
> > Return `true` if HUD is shown on this entity

## CDynamicProp / C_DynamicProp

### Shared

### CDynamicProp

> 

### C_DynamicProp

CScriptProp / C_ScriptProp \-\-\-\-\-\-\-\-\-\--

### Shared

> 

### CScriptProp

> 

### C_ScriptProp

## CBaseCombatWeapon / C_BaseCombatWeapon

### Shared

> > Returns the weapon description

### CBaseCombatWeapon

### C_BaseCombatWeapon

## CWeaponX / C_WeaponX

Weapons hold by a player or that are lying on the ground are of this
type.

### Shared

> > Returns the owner of this weapon
>
> > Returns `true` if this weapon can deal crits
>
> > Returns the max damage at the maximum travel distance
>
> > Get a weapon setting
>
> > Get a weapon setting
>
> > Get a weapon setting
>
> > Return the amount of ammo in a weapon
>
> > Returns the amount of clips remaining in a weapon
>
> > Returns the maximum ammo in a clip of a primary weapon
>
> > Returns `true` if this weapon is a charge weapon
>
> > You need to set a game time as time.
>
> > Returns the weapon class name
>
> > Get all mods of this weapon
>
> > Returns `true` if this weapon is equipped as a offhand weapon
>
> > Returns the percent this weapon has been charged
>
> > Returns the time this weapon needs to be charged
>
> > Check if the array of mods for this weapon contains `mod`
>
> > Returns the amount of energy consumed per use.
>
> > Set the mods this weapon.
>
> > Returns a bitflag of damage types this weapon has.
>
> > Returns script flags of this weapon.
>
> > Returns `true` if clients should be predicting the projectiles fired
> > from this weapon.
>
> > Returns the script time of this weapon.
>
> > `gameTime` needs to be game time. The current game time can be
> > retrieved with `Time()`
>
> > Returns `true` if this weapon is currently being reloaded.
>
> > Force the holder to ADS this weapon.
>
> > Allow the holder to hipfire.
>
> > Set the ammo of a primary weapon.
>
> > Stops the effects.
>
> > Reload progress. Reloading continues from there.
>
> > Returns the amount of ammo that is being used per shot.
>
> > Allow entities to use the weapon.
>
> > Remove the passed mod from this weapon.
>
> > Play a sound on this weapon.
>
> > Returns `true` if this weapon is in ADS.
>
> > Reset the amount of energy consumed per use
>
> > Set the amount of energy consumed per use.
>
> > Fires a hitscan bullet from this weapon.
>
> > Returns `true` while the ADS button is pressed.
>
> > Returns `true` if the weapon can be fired.
>
> > Add a mod to this weapon
>
> > Check if weaponType is valid:
> > `Assert( weaponType in VALID_WEAPON_TYPES )`
>
> > Note that fuse time of 0 means the grenade won\'t explode on its
> > own, instead it depends on OnProjectileCollision() functions to be
> > defined and explode there.

### CWeaponX

> > Force this weapon to dry fire
>
> > Play an effect on the weapon owner
>
> > Will eventually result in `Grenade_OnWeaponToss_()` or equivalent
> > function
>
> > returns `true` if this weapon has been forced to be released

### C_WeaponX

> > the second asset is probably the third person effect played.
>
> > `index` may be the number of rounds in the clip etc.

## CProjectile / C_Projectile

Projectiles.

### Shared

> > Returns an array of every mod this projectile has equipped
>
> > Set the projectile trail by index
>
> > Set the time after which this projectile gets destroyed
> > programmatically
>
> > Only use reduced effects for this projectile
>
> > Tells the code that the projectile was refired from the vortex so
> > that it uses \"projectile_vortex_vscript\"
>
> > Get the gametime when this projectile has been created

### CProjectile

> 

### C_Projectile

## CBaseGrenade / C_BaseGrenade

Grenade entities in worldspace. Grenades that are equipped (\"cooked\")
by players are instances from the CWeaponX class.

### Shared

> > Get the damage radius
>
> > Get the explosion radius
>
> > Explode this grenade now
>
> > Get the entity that has thrown this grenade
>
> > Returns `true` if this grenade has already been ignited

### CBaseGrenade

> > Set fuse time for this grenade
>
> > Set the ignition duration for this grenade

### C_BaseGrenade

## CMissile / C_Missile

### Shared

> > Make this missile explode now
>
> > If both `slowAndExpand` and `consistentSpacing` are true, missiles
> > fly faster instead of normal `slowAndExpand` behavior.

### CMissile

### C_Missile

## CPlayer / C_Player

### Shared

> > Returns the gen of the player account.
>
> > Returns the level of the player account.
>
> > Returns the xp of the player account.
>
> > Returns `true` if the player is currently lunging to a melee victim.
>
> > Returns the player account name
>
> > Returns the score of the player in the provided category. some
> > categories are: PGS_KILLS, PGS_DEATHS, PGS_SCORE etc.
>
> > Returns the soul of the player\'s autotitan.
>
> > Returns the index of the selected burn card.
>
> > Use `GetActiveBurnCardIndex` instead
>
> > Returns the angles of this player\'s camera.
>
> > Returns `true` if the player is wall hanging.
>
> > Returns `true` if the player is crouching.
>
> > Returns `true` if the player is standing
>
> > Returns `true` if the player is wallrunning.
>
> > Returns `true` if the player is currently attached to a zipline
>
> > Returns the camera position of this player.
>
> > Y Axis
>
> > X Axis
>
> > Holsters this weapon. The player can\'t use it until it\'s deployed
> > again with `DeployWeapon`
>
> > May not work with `DeployAndEnableWeapons()` and
> > `HolsterAndDisableWeapons()`
>
> > Returns the fractal of the current weapon zoom. 1.0 is fully zoomed
> > in.

### CPlayer

> > Force this player to stand up
>
> > Allow crouching
>
> > Decoy Types: `pt_mp_execution_attacker_hologram_01`,
> > `pt_mp_execution_attacker_hologram_02`,
> > `pt_mp_execution_attacker_hologram_03`
>
> > Force this player to crouch.
>
> > Allow this player to stand.
>
> > Returns `true` if noclip is enabled.
>
> > Allows the player to double jump again.

### C_Player

> > Executes a command on the player\'s client. For a server to execute
> > a console command on a client, the client has to launch the game
> > with the `norestrictservercommands` launch argument for security
> > reasons.
>
> > If called without paramets returns time for the player\'s titan
> > drop.
>
> > play a jolt effect on the player
>
> > Disable showing crosshair names of entities when aiming at them.
>
> > Enable showing crosshair names of entities when aiming at them.
> > (default)
>
> > Stop player input.

## CTitanSoul / C_TitanSoul

### Shared

> > Returns `true` if this soul is in doomed state
>
> > Returns an instance of `CNPC_Titan`

### CTitanSoul

> 

### C_TitanSoul

## CBaseCombatCharacter / C_BaseCombatCharacter

### Shared

> > Returns the first rodeo rider found or null if there are none.
>
> > Returns number of rodeo slots available on this entity.
>
> > Returns rodeo rider (if there is one) at the given slot.

### CBaseCombatCharacter

> > Looks for \"headshotFX\" in an AI settings file or a player set file
>
> > Sets the maximum number of rodeo slots available on this entity.
>
> > Sets the rodeo rider at the given slot

### C_BaseCombatCharacter

> 

## CAI_BaseNPC / C_AI_BaseNPC

### Shared

> > Expect as string
>
> > `AIC_SMALL_TURRET`, `AIC_MARVIN`, `AIC_SPECTRE`,
> > `AIC_STALKER_CRAWLING`, `AIC_FRAG_DRONE`, `AIC_HUMAN`
>
> > get the current flying speed of the npc.

### CAI_BaseNPC

> > Possible behaviours: `Follow`, `Assault`
>
> > Clears the enemy of this npc.
>
> > Sets the enemy this npc will attack.
>
> > Max pilot engagement distance
>
> > Max titan engagement distance
>
> > Sets if a capability is available to the player
>
> > Returns `true` if the npc can see the `ent`.
>
> > Freezes all animations and movement of this entity.
>
> > unfreezes all animations and movement of this entity.
>
> > Returns if `this.supportsXRay` not null.
>
> > Force into combat state by updating NPC\'s memory of the player.
>
> > Returns true if NPC is in combat.

### C_AI_BaseNPC

## CNPC_Titan / C_NPC_Titan

### Shared

> 

### CNPC_Titan

> 

### C_NPC_Titan

## CNPC_Dropship / C_NPC_Dropship

### Shared

> 

### CNPC_Dropship

### C_NPC_Dropship

## CNPC_Drone

> > Set to `false` to not attack enemies.

CNPC_SentryTurret / C_NPC_SentryTurret

### Shared

> 

### CNPC_SentryTurret

> 

### C_NPC_SentryTurret

## CFirstPersonProxy / C_FirstPersonProxy

### Shared

### CFirstPersonProxy

### C_FirstPersonProxy

## CBaseAnimating / C_BaseAnimating

### Shared

> 

### CBaseAnimating

> 

### C_BaseAnimating

> 

## CPlayerDecoy / C_PlayerDecoy

### Shared

### CPlayerDecoy

> > Dissolve this decoy. You might want to clear decoy fx with
> > `CleanupFXAndSoundsForDecoy( entity decoy )` afterwards.
>
> > Set the time after which the decoy gets automatically dissolved.
>
> > Sets if friendly fire is enabled for this decoy.
>
> > Sets if this decoy gets killed when colliding with props or
> > geometry.

### C_PlayerDecoy

## CTurret

> 

## C_Titan_Cockpit

> > Returns the total time of time spent in this cockpit.
> >
> > Cockpit booting takes 1.3 seconds, so anything less than 1.3 seconds
> > is still playing the booting animation. You can use
> > `TitanCockpit_IsBooting( entity cockpit )` to determine this state.

## CParticleSystem

> 

## CVortexSphere / C_VortexSphere

### Shared

> 

### CVortexSphere

> 

### C_VortexSphere

## CEnvExplosion
