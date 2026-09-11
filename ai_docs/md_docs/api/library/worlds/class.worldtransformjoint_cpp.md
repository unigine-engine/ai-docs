# Unigine.WorldTransformJoint Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


This class is used to create [joint transforms](../../../objects/worlds/world_transforms/transform_bone/index.md). It should have *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* or *[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)* as a parent. You should specify a [joint](#setJointName_cstr_void) that will be used for its transformations. For other nodes to move along with these transformations, they should be assigned as *WorldTransformJoint* children.


### See Also


UnigineScript sample


## WorldTransformJoint Class

### Members

## void setJointName ( const char * name )

Sets a new name of the joint used for transformation.
### Arguments

- *const char ** **name** - The name of the joint.

## const char * getJointName () const

Returns the current name of the joint used for transformation.
### Return value

Current name of the joint.
---

## static WorldTransformJointPtr create ( const char * name = 0 )

Constructor. Creates a *WorldTransformJoint* in the world coordinates with a specified joint name.
### Arguments

- *const char ** **name** - Name of the joint.

## static int type ( )

Returns the type of the node.
### Return value

*[World](../../../api/library/engine/class.world_cpp.md)* type identifier.
