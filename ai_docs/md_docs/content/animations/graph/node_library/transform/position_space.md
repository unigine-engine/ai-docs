# Position Space


![](../img/position_space.png)

### Description

Re-expresses a **position** in another coordinate space. The node takes a point in the space set by the **From** property and outputs the same point in the space set by the **To** property. Both the rotation and the translation of the frame are applied, which is what tells this node apart from [Direction Space](../../../../../content/animations/graph/node_library/transform/direction_space.md).


The usual case is feeding a world-space point from gameplay code into a solver that expects object space: set **From** to World and **To** to Object, and wire the result into the **Target** input of an [Two Bone IK](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) or [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **In** | The position to convert, expressed in the **From** space. |
| ![](../img/types/anim_pose.png) | **Pose** | The pose the joint frames are taken from. It is required only when **From** or **To** is set to Local; for a World-to-Object conversion the input may be left unconnected. |
| ![](../img/types/vec3.png) | **Out** | The same position expressed in the **To** space. |


## Properties


| From | Space the incoming value is currently expressed in: World, Object (relative to the skeleton root), or Local (relative to the parent of the joint picked in **From Joint**). The default value is World. |
|---|---|
| To | Space the value is converted to. The same three options as **From**. The default value is Object. |
| From Joint | Joint whose local frame the incoming value is expressed in. Shown only when **From** is set to Local. |
| To Joint | Joint whose local frame the value is converted to. Shown only when **To** is set to Local. |


## See Also


- [Direction Space](../../../../../content/animations/graph/node_library/transform/direction_space.md) for vectors that carry a direction only.
- [Rotation Space](../../../../../content/animations/graph/node_library/transform/rotation_space.md) for quaternions.
- [Get Joint Transform](../../../../../content/animations/graph/node_library/transform/get_joint_transform.md) and [Set Joint Transform](../../../../../content/animations/graph/node_library/transform/set_joint_transform.md).
