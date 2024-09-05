# NPCs

For settings, see `AI Settings <ai-settings>`s

> Controls if `ent` is traversable by NPCs

## NPC Squads

## NPC Navigation Nodes

> Returns a node index

> Returns a node index

## Navmeshes

> Clamps a goal point to the NavMesh for a given AI. Uses AIs hull size
> as test extents

> Clamps a goal point to the NavMesh for a given AI. As extents increase
> in size more possible clamp positions become available, but too large
> and the clamped position may be very far from the original point.

> Clamps a goal point to the NavMesh for a given hull

> Clamps a goal point to the NavMesh for a given hull. As extents
> increase in size more possible clamp positions become available, but
> too large clamped position may be very far from the original point.

> Get nearby ground positions by following the NavMesh graph

> Get n( \< 64 ) ground positions around a spot within `minDist` and
> `maxDist`

> Get up to n ground positions around a spot within `minDist` and
> `maxDist`. Gets center of random polygons.

> Checks if the npc can reach the position over graph

## Skits

> Get skit nodes sorted by nearest to average player position with some
> randomization

> Get skit nodes sorted by nearest to hardpoints with some randomization

> Get skit nodes sorted by nearest to pos with some randomization

## Dangerous Areas

> Create a known dangerous are that AI should avoid if necessary. The
> lifetime of the danger is tied to an entity

> Same as AI_CreateDangerousArea except the origin is always in a single
> place

> Create dangerous area using damage def

## AIN

[AIN on the valve wiki](https://developer.valvesoftware.com/wiki/AIN)

## Spawners

> Get array of spawners matching a class name

> Get array of spawners matching a script name
