# Threads, Signals and Flags {#async-doc}

## Threads

Squirrel allows scripts to spin off function calls in a thread. All
subsequential function calls will be threaded as well.

In threaded functions, it\'s possible to halt a threaded function with
`wait` statements, signals, flags and by suspending a thread object.

You can use the `IsNewThread()` function to determine if the current
function is threaded off.

For more information, check out the [squirrel documentation on
threads](http://www.squirrel-lang.org/squirreldoc/reference/language/threads.html)
and [sq functions of
threads](http://www.squirrel-lang.org/squirreldoc/reference/language/builtin_functions.html#thread).
SquirrelRe is very similar to vanilla squirrel in this regard.

A thread is considered finished, after the threaded function returned a
value. This may be `null`.

### Spinning off a thread

To create a new coroutine, call a function with the `thread` keyword
before.

```squirrel
thread void function(){}()
thread MyFunction()
```

To get a thread object, use the `newthread` function.

```squirrel
void function CoroutineExample()
{
    suspend( "passback" ) // passback is optional
    print( "threaded statement" )
}

var co = newthread( CoroutineExample )
var suspendedReturn = co.call() // you NEED to use .call, invoking the function with () won't work
co.wakeup() // continue thread
```

### wait

The `wait` statement halts threads for a set amount of time specified
after the `wait` keyword. Integers and floats are accepted as times in
seconds.

```squirrel
void function WaitExample( float n )
{
    wait 1 // wait 1 second
    wait n // wait n seconds
}

thread WaitExample( 0.5 ) // thread will halt for a total 1.5 seconds
```

To wait a single frame, don\'t use `wait 0` since it doesn\'t actually
wait a game frame. For example, if you have a client loop that does wait
0 even if the game is paused the loop will still run. Use `WaitFrame()`
instead.

When using infinite loops it\'s important to work with `wait` statements
to avoid the game freezing.

If you want to wait until a thread is finished, you can spin off the
thread that you wait for with the `waitthread` keyword.

```squirrel
void function ParentThread()
{
    printt( "pre spinoff " + string( Time() ) )
    waitthread void function()
    {
        printt( "mid spinoff " + string( Time() ) )
        wait 1
    }
    printt( "post spinoff" + string( Time() ) )
}
```

### OnThreadEnd

Use the `OnThreadEnd` function to execute a callback after a thread has
ended. This is useful for cleanup functions that remove entities after
they\'re used or similar.

```squirrel 
void function PlayIncomingFX( vector origin, int teamNum )
{
    wait 1.50
    EmitSoundAtPosition( teamNum, origin, "Titan_1P_Warpfall_Start" )

    local colorVec = Vector( 0, 255, 0 )
    entity cpoint = CreateEntity( "info_placement_helper" )
    SetTargetName( cpoint, UniqueString( "pickup_controlpoint" ) )
    DispatchSpawn( cpoint )
    cpoint.SetOrigin( colorVec )
    entity glowFX = PlayFXWithControlPoint( INCOMING_SPAWN_FX, origin, cpoint, -1, null, null, C_PLAYFX_LOOP )

    OnThreadEnd(
        function() : ( glowFX, cpoint )
        {
            if ( IsValid( glowFX ) )
                glowFX.Destroy()
            if ( IsValid( cpoint ) )
                cpoint.Destroy()
        }
    )

    wait 1.25
}
```

### Example Script

```squirrel
void function SetPositionDelayed( entity ent, vector pos, float delay )
{
    wait delay
    ent.SetOrigin( pos )
}

SetPositionDelayed( player, <0, 0, 100>, 5.0 )
SetPositionDelayed( player, <0, 0, 50>, 2.5 ) // this will finish sooner.
```

## Signals and flags

Signals and flags allow threads to wait for events before running some
code.

### Signals

> Registers a Signals to use on any entity. It\'s required to register
> signals before using them.

> `../reference/respawn/entities` 
>
> Trigger a signal on this entity. The passed `results` will be returned
> by `WaitSignal`.
>
> Ends this thread when the identifier is signaled on this entity
>
> Halts this thread until a signal is activated for this entity
>
> > Register a callback that executes when the `signal` has been fired
> > on this Entity
>
> > Disconnects the callback from the signal.
>
> Connects an output on this entity to an input on another entity via
> code. The `target` can be a name or a named entity.
>
> Fire a signal on this entity, with optional parm and delay
>
> Fire a signal on this entity, with optional parm and delay
> (synchronous)

It\'s also possible to trigger and catch signals with methods that
aren\'t properties of an entity.

> Trigger a signal on `ent`. The passed `results` will be returned by
> `WaitSignal`.

> Wait for any of the passed signals to be triggered.
>
> ```squirrel
> // Wait for the NPC to die, delete, or get leeched, then remove the npc from the array
> WaitSignal( ent, "OnDeath", "OnDestroy", "OnLeeched" )
> ```

> Ends this thread when the identifier is signaled on `ent`

#### Example

For example, if we want to tell a player not to give up after being
killed several times, we can write it this way:

```squirrel
// First, we register signal we want to use
RegisterSignal("OnMultipleDeaths")


void function WatchForDeaths (entity player) 
{
    int deathsCount = 0

    while( GamePlayingOrSuddenDeath() )
    {
        if ( player.isDead() )  // This doesn't exist, don't try this at home
        {
            deathsCount += 1

            if (deathsCount >= 42)
            {
                // This sends "OnMultipleDeaths" signal on player entity
                player.Signal( "OnMultipleDeaths" )
            } 
        }
    }
}


void function DontGiveUp (entity player)
{
    // This is a blocking call
    player.WaitSignal("OnMultipleDeaths");

    // This will not run until entity received "OnMultipleDeaths" signal
    SendHudMessage( player, "Don't give up!", -1, 0.4, 255, 0, 0, 0, 0, 3, 0.15 )
}

// Launch our methods in dedicated threads
entity player = GetPlayerArray()[0]
thread WatchForDeaths( player )
thread DontGiveUp( player )
```

In this example, the `DontGiveUp` method is launched at the same time as
`WatchForDeaths`; but it will not run until player died 42 times.

When you want your thread to die on a given event, you can use
`entity.EndSignal( "OnMultipleDeaths" )`; when said signal is set,
thread will end (after calling any OnThreadEnd methods).

### Flags

`Flags` work pretty much the same way as `Signals`, except they can be
set up without target entity:

> Create a flag

> Halts a thread until a flag is set. Callee must be threaded off.

> Halts until every passed flag is set. Callee must be threaded off.

> Halts until the passed flag is set or the timer runs out. Callee must
> be threaded off.

> Raise a flag

> Set `flagset` after `flagwait` is set and the delay is met.

> Reset a flag

> Resets all passed flags.

> Reset `flagclear` when `flagwait` is set.

> Resets a flag after the timer runs out.

> Wait until any passed flag is cleared.

> Raise a flag if it is reset, or reset it if it\'s raised.

> Ends this thread when the flag is set

> Returns the current state of a flag.

> Returns `true` if the flag is initialized

> Splits the flag on `" "`

> Splits the value of the keyvalues of the entity on the index `field`
> on `" "`

#### Example

```squirrel
void function FlagExample()
{
    FlagInit( "BombHasExploded" )

    thread BombTicker()

    FlagWait( "BombHasExploded" )
    print( "bomb just exploded" )
}

void function BombTicker()
{
    Assert( IsNewThread(), "BombTicker must be threaded off" )
    wait RandomFloatRange( 3, 9 )
    FlagSet( "BombHasExploded" )
}
```
