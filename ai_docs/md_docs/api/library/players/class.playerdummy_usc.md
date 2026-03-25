# Unigine.PlayerDummy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Player


This class is used to create a dummy camera that is a simple viewport into the world. It has no physical properties and cannot collide with objects.


### See Also


- C++ sample
- C# component samples:

  -
  -
- UnigineScript sample


## PlayerDummy Class

### Members

---

## static PlayerDummy ( )

Constructor. Creates a new dummy player.
## void setViewDirection ( vec3 direction )

Sets a new Player's view direction vector.
### Arguments

- *vec3* **direction** - New view direction vector to be set.

## vec3 getViewDirection ( )

Returns the current Player's view direction vector.
### Return value

Current Player's view direction vector.
## static int type ( )

Returns the type of the player.
### Return value

PlayerDummy [type identifier](../../../api/library/nodes/class.node_usc.md#PLAYER_DUMMY).
