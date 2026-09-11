# Unigine.WorldTransformJoint Class (CS)

**Inherits from:** Node


This class is used to create [joint transforms](../../../objects/worlds/world_transforms/transform_bone/index.md). It should have *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* or *[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md)* as a parent. You should specify a [joint](#setJointName_cstr_void) that will be used for its transformations. For other nodes to move along with these transformations, they should be assigned as *WorldTransformJoint* children.


### See Also


UnigineScript sample


## WorldTransformJoint Class

### Properties

## string JointName

The name of the joint used for transformation.
### Members

---

## WorldTransformJoint ( string name = 0 )

Constructor. Creates a *WorldTransformJoint* in the world coordinates with a specified joint name.
### Arguments

- *string* **name** - Name of the joint.

## static int type ( )

Returns the type of the node.
### Return value

*[World](../../../api/library/engine/class.world_cs.md)* type identifier.
