# Unigine.PlayerDummy Class (CPP)

**Header:** #include <UniginePlayers.h>

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

## static PlayerDummyPtr create ( )

Constructor. Creates a new dummy player.
## void setViewDirection ( const Math:: vec3 & direction )

Sets a new Player's view direction vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - New view direction vector to be set.

## Math:: vec3 getViewDirection ( ) const

Returns the current Player's view direction vector.
### Return value

Current Player's view direction vector.
## static int type ( )

Returns the type of the player.
### Return value

PlayerDummy [type identifier](../../../api/library/nodes/class.node_cpp.md#PLAYER_DUMMY).
