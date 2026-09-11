# ObjectExtern Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


ObjectExtern is a custom user-defined object created via API.


### See Also


C++ sample


## ObjectExtern Class

### Members

## void setMaterialNodeType ( int type )

Sets a new [node type](../../../api/library/nodes/class.node_usc.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN).
> **Notice:** As ObjectExtern is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Arguments

- *int* **type** - The node type to be used by the renderer to determine which materials can be applied to the object

## int getMaterialNodeType () const

Returns the current [node type](../../../api/library/nodes/class.node_usc.md) to be used by the renderer to determine which materials can be applied to the object. One of the [node type identifiers](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN).
> **Notice:** As ObjectExtern is a custom user-defined object, so the user should determine the node type for the renderer to treat this object properly. Setting inappropriate node type may lead to system crashes.


### Return value

Current node type to be used by the renderer to determine which materials can be applied to the object
---

## static ObjectExtern ( int class_id )

Constructor. Creates a custom user-defined object.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( )

Returns the unique class ID of the object.
### Return value

Class ID if the object exists; otherwise, 0.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectExtern](../../../api/library/nodes/class.node_usc.md#OBJECT_EXTERN) type identifier.
