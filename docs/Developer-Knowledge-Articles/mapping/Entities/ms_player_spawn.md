# ms_player_spawn Entity

## Properties

* message "messageString"

    - Determines the transition this entity is tied to

* target "trigger on spawn"

    - Targets this entity whenever a player spawns here

* angles

    - Rotation of the player at spawntime.

(Note that whenever a player spawns, the map event "player_spawned" fires, and whenever a new player joins the server, "player_joined" fires, you can use these events to trigger entities that need to be active after players first arrive.)

You'll need at least one of these in your map. The messageString should be the same as the desttrans of as the msarea_transition that points to it. If there is no msarea_transition leading to this map, use the name of the current map instead.

```cpp title="Example: Edana's ms_player_spawn" linenums="1"
 {
"message" "a3trans"
"classname" "ms_player_spawn"
}
```


