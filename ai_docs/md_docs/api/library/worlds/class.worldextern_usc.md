# Unigine.WorldExtern Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


WorldExtern is a custom user-defined world created via API.


## WorldExtern Class

---

## static WorldExtern ( Node node )

Constructor.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node instance.

## static WorldExtern ( int class_id )

Constructor. Creates a custom user-defined world.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( )

Returns a unique class ID.
### Return value

Returns a unique class ID if the world exists; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[WorldExtern](../../../api/library/nodes/class.node_usc.md#WORLD_EXTERN) type identifier.
