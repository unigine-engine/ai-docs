# Unigine::IKInfoTwoBone Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** IKInfo


This class stores the parameters of the analytical IK solver for a three-joint chain, such as shoulder-elbow-wrist or hip-knee-ankle. The solver bends the root and the mid joints so that the end joint reaches toward the target. A chain like this bends in one plane, so there is exactly one correct pose for a given target and the solver finds it in a single step, without iterations.


The three joints are picked explicitly, so any hierarchy works, including twist or helper bones placed between them. The rotation of the end joint is not modified: set it separately after solving if the orientation of the wrist or the foot matters.


An instance of this class is passed to the *[solveLayerTwoBoneIK()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerTwoBoneIK_int_IKInfoTwoBone_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class.


The same solver is available as the [Two Bone IK](../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## IKInfoTwoBone Class

### Members

## void setRootJoint ( int joint )

Sets a new index of the joint the chain starts at, typically a shoulder or a hip. The default value is -1.
### Arguments

- *int* **joint** - The index of the joint the chain starts at

## int getRootJoint () const

Returns the current index of the joint the chain starts at, typically a shoulder or a hip. The default value is -1.
### Return value

Current index of the joint the chain starts at
## void setMidJoint ( int joint )

Sets a new index of the joint that bends, typically an elbow or a knee. It must be a descendant of the root joint. The default value is -1.
### Arguments

- *int* **joint** - The index of the joint that bends

## int getMidJoint () const

Returns the current index of the joint that bends, typically an elbow or a knee. It must be a descendant of the root joint. The default value is -1.
### Return value

Current index of the joint that bends
## void setEndJoint ( int joint )

Sets a new index of the end effector that reaches for the target, typically a wrist or an ankle. It must be a descendant of the mid joint. Its rotation is not modified by the solver. The default value is -1.
### Arguments

- *int* **joint** - The index of the end effector

## int getEndJoint () const

Returns the current index of the end effector that reaches for the target, typically a wrist or an ankle. It must be a descendant of the mid joint. Its rotation is not modified by the solver. The default value is -1.
### Return value

Current index of the end effector
## void setUsePole ( bool pole )

Sets a new value indicating if the pole is used to control the bending direction of the chain. When disabled, the chain keeps the bending plane of the input pose. The default value is false.
### Arguments

- *bool* **pole** - Set **true** to enable the pole is used to control the bending direction; **false** - to disable it.

## bool isUsePole () const

Returns the current value indicating if the pole is used to control the bending direction of the chain. When disabled, the chain keeps the bending plane of the input pose. The default value is false.
### Return value

**true** if the pole is used to control the bending direction; otherwise **false**.
---

## static IKInfoTwoBonePtr create ( )

Constructor. Creates a new set of two-bone IK parameters with default values.
