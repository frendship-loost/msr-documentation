# msarea_transition Entity


## Properties

* destname "Title of Destination" (eg. "Helena Under Siege" - do not use quotes in title)

    - This is the name the player will see when the transition makes its pop-up

* destmap "destination bsp" (sans the ".bsp", eg "Helena")

    - This is the map the transition will change to/vote for when activated

* desttrans "messageString" ("message" property of ms_player_spawn on destination map, see below)

    - Which spawn to use on the destination map

* targetname "messageString" ("message" property of ms_player_spawn on this map, see below)

    - Which spawn to use on this map after this transition is touched

!!! info "Important:"
    This is a brush entity. If used as a point entity, only one player will be able to use it at a time.

## Desttrans Property Details

Desttrans is the tricky part, it must match the "message" property of an ms_player_spawn on the receiving map. Otherwise, the players will be kicked from the new map upon connect. Targetname, on the other hand, should match the "message" property of an ms_player_spawn on the current map (ie. the map the msarea_transition is actually in - preferably the one nearest to it). If a player dies after touching an msarea_transition, they will respawn at the ms_player_spawn entity matching the transition's targetname.