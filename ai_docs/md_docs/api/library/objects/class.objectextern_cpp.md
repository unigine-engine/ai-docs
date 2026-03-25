# ObjectExtern Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


ObjectExtern is a custom user-defined object created via API.


### See Also


C++ sample


## ObjectExtern Class

### Members

---

## static ObjectExternPtr create ( int class_id )

Constructor. Creates a custom user-defined object.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( ) const

Returns the unique class ID of the object.
### Return value

Class ID if the object exists; otherwise, 0.
## void setMaterialNodeType ( int type )

Sets the node type to be used by the renderer to determine which materials can be applied to the object.
> **Notice:** As ObjectExtern is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Arguments

- *int* **type** - Node type ID. One of the [node type identifiers](../../../api/library/nodes/class.node_cpp.md#DECAL_BEGIN).

## int getMaterialNodeType ( ) const

Returns the node type to be used by the renderer to determine which materials can be applied to the object.
> **Notice:** As ObjectExtern is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Return value

Node type ID. One of the [node type identifiers](../../../api/library/nodes/class.node_cpp.md#DECAL_BEGIN).
## static int type ( )

Returns the type of the node.
### Return value

[ObjectExtern](../../../api/library/nodes/class.node_cpp.md#OBJECT_EXTERN) type identifier.
