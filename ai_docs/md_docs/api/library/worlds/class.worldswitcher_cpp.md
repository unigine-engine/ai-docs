# Unigine.WorldSwitcher Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


This class allows switching off (and turn on) big parts of the world at once. A *Switcher* is made a parent for nodes it controls. It is of a box shape, and the distance from the camera can be measured to its edges or to its center.


### See Also


UnigineScript sample


## WorldSwitcher Class

### Members

## void setMaxDistance ( float distance )

Sets a new maximum distance of visibility. if a camera is further from a node than this maximum distance, a node is not visible. the default is inf.
### Arguments

- *float* **distance** - The maximum distance of visibility, in units.

## float getMaxDistance () const

Returns the current maximum distance of visibility. if a camera is further from a node than this maximum distance, a node is not visible. the default is inf.
### Return value

Current maximum distance of visibility, in units.
## void setMinDistance ( float distance )

Sets a new minimum distance of visibility. if a camera is closer to a node than this minimum distance, a node is not visible. the default is -inf.
### Arguments

- *float* **distance** - The minimum distance of visibility, in units.

## float getMinDistance () const

Returns the current minimum distance of visibility. if a camera is closer to a node than this minimum distance, a node is not visible. the default is -inf.
### Return value

Current minimum distance of visibility, in units.
---

## static WorldSwitcherPtr create ( )

Constructor. Creates a *World Switcher*.
## static int type ( )
