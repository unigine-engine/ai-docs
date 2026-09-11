# Joint Limit Set


![](../img/joint_limit_set.png)

### Description

Aggregates several joint limit nodes into a single constraint reference. The node does not modify the pose itself: it bundles the **Limit** outputs of individual joint limit nodes and exposes them as one **Set** output, which is then connected to the **Limits** input of an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md). When a set is connected, the chain reads the aggregated limits from it.


Connect a joint limit node to any input pin. The node shows the connected pins plus one trailing empty pin, and grows as you wire more limits in.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/constraint.png) | **Limit 1** | A joint limit to include in the set. Accepts the **Limit** output of any joint limit node. |
| ![](../img/types/constraint.png) | **Limit 2** | A joint limit to include in the set. |
| ![](../img/types/constraint.png) | **Limits** | The aggregated constraint reference. Connect it to the **Limits** input of an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md). |


## Notes


The number of input pins grows as you connect limits: only the connected pins and a single trailing empty pin are shown on the node. The number of limits in a set is not capped.


## See Also


- [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) and [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md) nodes that consume the set.
- The joint limit nodes: [Joint Hinge Limit](../../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md), [Joint Cone Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md), [Joint Cone Asym Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md), [Joint Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md), [Joint Hinge Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md), [Joint Cone Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md), [Joint Cone Asym Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_twist_limit.md).
- The [JointLimitSetInfo](../../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) class used to configure the same aggregation from the API.
