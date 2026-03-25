# Unigine.WorldExtern Class (CS)

**Inherits from:** Node


WorldExtern is a custom user-defined world created via API.


## WorldExtern Class

### Members

---

## WorldExtern ( Node node )

Constructor.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node instance.

## WorldExtern ( int class_id )

Constructor. Creates a custom user-defined world.
### Arguments

- *int* **class_id** - Unique class ID.

## int GetClassID ( )

Returns a unique class ID.
### Return value

Returns a unique class ID if the world exists; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[WorldExtern](../../../api/library/nodes/class.node_cs.md#WORLD_EXTERN) type identifier.
