# Unigine.WorldExtern Class (CPP)

**Header:** #include <UnigineWorld.h>

**Inherits from:** Node


WorldExtern is a custom user-defined world created via API.


## WorldExtern Class

---

## static WorldExternPtr create ( const Ptr < Node > & node )

Constructor.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to Node.

## static WorldExternPtr create ( int class_id )

Constructor. Creates a custom user-defined world.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( ) const

Returns a unique class ID.
### Return value

Returns a unique class ID if the world exists; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[WorldExtern](../../../api/library/nodes/class.node_cpp.md#WORLD_EXTERN) type identifier.
