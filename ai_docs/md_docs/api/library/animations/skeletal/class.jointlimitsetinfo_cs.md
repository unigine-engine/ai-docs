# Unigine::JointLimitSetInfo Class (CS)


This class bundles several joint limits into a single object that is handed to a chain solver. It does not modify the pose itself: assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md), and the solver reads the per-joint limits from it on every iteration. There is no cap on the number of limits in a set.


The set holds limits of any of the seven types - see [JointLimitInfo](../../../../api/library/animations/skeletal/class.jointlimitinfo_cs.md). The set is owned by the caller and must outlive the solve.


The debug visualization of a whole set is drawn by the *[RenderLayerJointLimitSetDebug()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointLimitSetDebug_int_JointLimitSetInfo_Mat4_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class.


The same solver is available as the [Joint Limit Set](../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitSetInfo Class

### Properties

## 🔒︎ int NumLimits

The number of joint limits in the set.
### Members

---

## JointLimitSetInfo ( )

Constructor. Creates a new empty set of joint limits.
## void AddLimit ( JointLimitInfo limit )

Adds a joint limit of any type to the set. A solver gives each joint a single slot, so adding two enabled limits for the same joint leaves only one of them in effect - the seven limit types already cover every swing and twist combination, so pick the one that fits instead.
### Arguments

- *JointLimitInfo* **limit** - Joint limit to add to the set.

## JointLimitInfo GetLimit ( int num )

Returns the joint limit at the given index in the set. Check the *[Type](../../../../api/library/animations/skeletal/class.jointlimitinfo_cs.md#getType_int)* value to find out which of the concrete limit types it is.
### Arguments

- *int* **num** - Index of the joint limit in the set.

### Return value

Joint limit at the given index.
## void ClearLimits ( )

Removes all the joint limits from the set.
