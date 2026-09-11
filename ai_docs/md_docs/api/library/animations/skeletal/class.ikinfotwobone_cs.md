# Unigine::IKInfoTwoBone Class (CS)

**Inherits from:** IKInfo


This class stores the parameters of the analytical IK solver for a three-joint chain, such as shoulder-elbow-wrist or hip-knee-ankle. The solver bends the root and the mid joints so that the end joint reaches toward the target. A chain like this bends in one plane, so there is exactly one correct pose for a given target and the solver finds it in a single step, without iterations.


The three joints are picked explicitly, so any hierarchy works, including twist or helper bones placed between them. The rotation of the end joint is not modified: set it separately after solving if the orientation of the wrist or the foot matters.


An instance of this class is passed to the *[SolveLayerTwoBoneIK()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerTwoBoneIK_int_IKInfoTwoBone_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class.


The same solver is available as the [Two Bone IK](../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## IKInfoTwoBone Class

### Properties

## int RootJoint

The index of the joint the chain starts at, typically a shoulder or a hip. The default value is -1.
## int MidJoint

The index of the joint that bends, typically an elbow or a knee. It must be a descendant of the root joint. The default value is -1.
## int EndJoint

The index of the end effector that reaches for the target, typically a wrist or an ankle. It must be a descendant of the mid joint. Its rotation is not modified by the solver. The default value is -1.
## bool UsePole

The value indicating if the pole is used to control the bending direction of the chain. When disabled, the chain keeps the bending plane of the input pose. The default value is false.
### Members

---

## IKInfoTwoBone ( )

Constructor. Creates a new set of two-bone IK parameters with default values.
