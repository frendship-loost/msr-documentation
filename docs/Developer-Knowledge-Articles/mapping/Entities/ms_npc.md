# ms_npc Entity


## Identical Entities

* msmonster_skeleton
* msmonster_troll
* msmonster_giantrat
* msmonster_giantbat
* msmonster_orcwarrior
* msmonster_orcberserker
* msmonster_orcarcher
* msmonster_orcranger

Any pointentity prefixed with msmonster_ will functionally be identical to ms_npc. Feel free to use the different named entities organizationally, since only their preview models and default scripts are different.

## Properties

* lives integer

    - number of times monster will respawn, if omitted or set zero, respawns forever.

* spawnchance [1-100]

    - chance of monster respawning with each spawn check, generally this should be 100%

* delaylow seconds

    - minimum time between spawn checks, in seconds

* delayhigh seconds

    - maximum time between spawn checks, in seconds

* spawnarea spawnAreaName

    - Ties monster to an msarea_monsterspawn (see below). Do not attempt to place monsters without monster spawns, it leads to issues.

* killtarget triggerString

    - [optional] Triggers this entity when monster dies. (It does not remove the target the way the same property of trigger_relay does)

* perishtarget triggerString

    - Trigger this when all lives are exhausted

* scriptfile scriptfile

    - determines monster/NPC type see list of applicable script files

!!! note
    Be aware that script names are cAsE sEnsItivE.

* descriptfile scriptfile

    - [optional] As above, but seems to be required for some monsters. Generally, it's best to leave this as the FGD sets it.

* nplayers integer - Only spawn this monster if there this number of players, or more, present (AUG2007 or later)

* reqhp integer - Only spawn this monster if the total HP of all players on the server is above this number (AUG2007 or later)

* title string-Change the monster's name to this (SEP2007a or later)

* dmgmulti float-Multiply the monster's damage by this factor (must be > 1, SEP2007a or later)

* hpmulti float-Multiply the monster's hitpoints by this factor (must be > 1, SEP2007a or later)

* params token-string-Additional Parameters to adjust the monster. (Usage of this system is explained here.)

* targetname targetString (used by other entities, such as ms_npcscript (below) or trigger relay, to target the monster )

* (angles, origin)