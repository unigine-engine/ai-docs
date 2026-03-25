# Unigine.WorldSwitcher Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


Interface for world switcher handling. See also the [UnigineScript analog](../../../api/library/worlds/class.worldswitcher_cpp.md).


### See Also


UnigineScript sample


## WorldSwitcher Class

### Members

---

## static WorldSwitcherPtr create ( )

Constructor. Creates a world switcher.
## void setMaxDistance ( float distance )

Sets the maximum distance of visibility. If a camera is further from a node than this maximum distance, a node is not visible. The default is inf.
### Arguments

- *float* **distance** - Maximum distance of visibility in units.

## float getMaxDistance ( ) const

Returns the current maximum distance of visibility. If a camera is further from a node than this maximum distance, a node is not visible. The default is inf.
### Return value

Maximum distance of visibility in units.
## void setMinDistance ( float distance )

Sets the minimum distance of visibility. If a camera is closer to a node than this minimum distance, a node is not visible. The default is -inf.
### Arguments

- *float* **distance** - Minimum distance of visibility in units.

## float getMinDistance ( ) const

Returns the current minimum distance of visibility. If a camera is closer to a node than this minimum distance, a node is not visible. The default is -inf.
### Return value

Minimum distance of visibility in units.
## static int type ( )
