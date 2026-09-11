# Unigine::JointLimitSetInfo Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>


This class bundles several joint limits into a single object that is handed to a chain solver. It does not modify the pose itself: assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md), and the solver reads the per-joint limits from it on every iteration. There is no cap on the number of limits in a set.


The set holds limits of any of the seven types - see [JointLimitInfo](../../../../api/library/animations/skeletal/class.jointlimitinfo_cpp.md). The set is owned by the caller and must outlive the solve.


The debug visualization of a whole set is drawn by the *[renderLayerJointLimitSetDebug()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointLimitSetDebug_int_JointLimitSetInfo_Mat4_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class.


The same solver is available as the [Joint Limit Set](../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitSetInfo Class

### Members

## int getNumLimits () const

Returns the current number of joint limits in the set.
### Return value

Current number of joint limits in the set
---

## static JointLimitSetInfoPtr create ( )

Constructor. Creates a new empty set of joint limits.
## void addLimit ( const Ptr<JointLimitInfo> & limit )

Adds a joint limit of any type to the set. A solver gives each joint a single slot, so adding two enabled limits for the same joint leaves only one of them in effect - the seven limit types already cover every swing and twist combination, so pick the one that fits instead.
### Arguments

- *const Ptr<JointLimitInfo> &* **limit** - Joint limit to add to the set.

## Ptr<JointLimitInfo> getLimit ( int num ) const

Returns the joint limit at the given index in the set. Check the *[getType()](../../../../api/library/animations/skeletal/class.jointlimitinfo_cpp.md#getType_int)* value to find out which of the concrete limit types it is.
### Arguments

- *int* **num** - Index of the joint limit in the set.

### Return value

Joint limit at the given index.
## void clearLimits ( )

Removes all the joint limits from the set.
