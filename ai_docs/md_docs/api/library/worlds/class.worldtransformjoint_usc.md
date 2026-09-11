# Unigine.WorldTransformJoint Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create [joint transforms](../../../objects/worlds/world_transforms/transform_bone/index.md). It should have *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)* or *[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md)* as a parent. You should specify a [joint](#setJointName_cstr_void) that will be used for its transformations. For other nodes to move along with these transformations, they should be assigned as *WorldTransformJoint* children.


### See Also


UnigineScript sample


## WorldTransformJoint Class

### Members

## void setJointName ( string name )

Sets a new name of the joint used for transformation.
### Arguments

- *string* **name** - The name of the joint.

## const char * getJointName () const

Returns the current name of the joint used for transformation.
### Return value

Current name of the joint.
---

## static WorldTransformJoint ( string name = 0 )

Constructor. Creates a *WorldTransformJoint* in the world coordinates with a specified joint name.
### Arguments

- *string* **name** - Name of the joint.

## static int type ( )

Returns the type of the node.
### Return value

*[World](../../../api/library/engine/class.world_usc.md)* type identifier.
