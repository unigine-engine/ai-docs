# Unigine.WorldSwitcher Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class allows switching off (and turn on) big parts of the world at once. A switcher is made a parent for nodes it controls. It is of a box shape, and the distance from the camera can be measured to its edges or to its center.


### See Also


UnigineScript sample


## WorldSwitcher Class

### Members

---

## static WorldSwitcher ( )

Constructor. Creates a world switcher.
## void setMaxDistance ( float distance )

Sets the maximum distance of visibility. If a camera is further from a node than this maximum distance, a node is not visible.
### Arguments

- *float* **distance** - Maximum distance of visibility in units.

## float getMaxDistance ( )

Returns the current maximum distance of visibility. If a camera is further from a node than this maximum distance, a node is not visible.
### Return value

Maximum distance of visibility in units.
## void setMinDistance ( float distance )

Sets the minimum distance of visibility. If a camera is closer to a node than this minimum distance, a node is not visible.
### Arguments

- *float* **distance** - Minimum distance of visibility in units.

## float getMinDistance ( )

Returns the current minimum distance of visibility. If a camera is closer to a node than this minimum distance, a node is not visible.
### Return value

Minimum distance of visibility in units.
## static int type ( )
