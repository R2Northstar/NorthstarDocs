# Server Authentification

!!! note
All of these functions are only exposed to the `UI` VM.
::::

These are functions required for the ingame server browser and the
authorization process for the Masterserver and game servers.

## Masterserver Authentification

> Returns `true` if the client is authenticated with the Masterserver

> Returns `true` if a successful connection has been established

## Game Server Authentification

> Tries authing with the fetched server at `serverIndex` and the
> provided password

> Returns `true` if the client is currently authing with a game server

# NSWasAuthSuccessful

> Returns `true` if the client successfully authed with a game server

> Tries to connect to the game server that has previously been
> authenticated with

> Returns the API reason why the last authentification failed

> Tries to authenticate with the local game server

> Call this after
> `NSWasAuthSuccessful <NSWasAuthSuccessful>` returns `true` to complete the local authorization
> process.

## Server Information

> Start fetching all available game servers from the Masterserver

> Returns `true` if the last request by

> Returns the total amount of fetched game servers

> Clears all fetched game servers

> Returns an array of all available Servers fetched from the
> Masterserver.

## Connection Callbacks

### AddConnectToServerCallback

> Add a callback to be executed right before connecting to a game server
> via the Server Browser

> Remove a function object from the list of callbacks

> Runs all callbacks that have been registered with
> `AddConnectToServerCallback <AddConnectToServerCallback>`

## Script Structs

> Contains all info about a game server.
>
> > Index of the native Object equivalent
>
> > ID assigned to the game server by the Masterserver in the
> > registration
>
> > Name of this game server
>
> > Description of this game server
>
> > Unlocalized name of the map that\'s currently running on the game
> > server
>
> > Unlocalized name of the playlist that\'s currently running on the
> > game server
>
> > The total amount of players currently connected to the player
>
> > The maximum amount of players that can connect to the server
>
> > If `true` an extra password is required to connect to the server.
> > Otherwise the password is an empty string
>
> > Unlocalized region where the physical server is located
>
> > Array of all mods that are required to be loaded on the client to be
> > able to join the server

> Information of a mod that has to be loaded on the client in order to
> join a game server
>
> > Name of the mod
>
> > Version of the mod
