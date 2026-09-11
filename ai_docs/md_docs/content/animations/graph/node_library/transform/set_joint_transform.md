# Set Joint Transform


![](../img/set_joint_transform.png)

### Description

Writes the position, rotation, and/or scale of a single joint into the incoming pose. Only the components with a connected input are modified: an unconnected input leaves the corresponding component unchanged from the input pose. The joint is selected via the **Joint** property, and the **Space** property controls whether the values are applied relative to the parent joint (local) or to the skeleton root (object). This node is commonly paired with the **[Get Joint Transform](../../../../../content/animations/graph/node_library/transform/get_joint_transform.md)** node.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to modify. |
| ![](../img/types/vec3.png) | **Position** | New joint position. When left unconnected, the position stays as in the input pose. The socket label reflects the current **Space** value (Position (Local Space) or Position (Object Space)). |
| ![](../img/types/quat.png) | **Rotation** | New joint rotation as a quaternion. When left unconnected, the rotation stays as in the input pose. The socket label reflects the current **Space** value. |
| ![](../img/types/vec3.png) | **Scale** | New joint scale. When left unconnected, the scale stays as in the input pose. The socket label reflects the current **Space** value. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the joint transform applied. |


## Properties


| Joint | The joint whose transform is written. Pick a joint from the skeleton of the mesh assigned to the graph. |
|---|---|
| Space | Coordinate space in which the transform is applied: Local (relative to the parent joint) or Object (relative to the skeleton root). The default value is Local. |


## See Also


- [Get Joint Transform](../../../../../content/animations/graph/node_library/transform/get_joint_transform.md)
