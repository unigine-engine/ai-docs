# Get Joint Transform


![](../img/get_joint_transform.png)

### Description

Reads the position, rotation, and scale of a single joint from the incoming pose. The joint is selected via the **Joint** property, and the **Space** property controls whether the values are read relative to the parent joint (local) or to the skeleton root (object). This node is typically used together with the **[Set Joint Transform](../../../../../content/animations/graph/node_library/transform/set_joint_transform.md)** node to read a joint transform, modify it, and write it back.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to read the joint transform from. |
| ![](../img/types/vec3.png) | **Position** | Position of the joint. The socket label reflects the current **Space** value (Position (Local Space) or Position (Object Space)). |
| ![](../img/types/quat.png) | **Rotation** | Rotation of the joint as a quaternion. The socket label reflects the current **Space** value. |
| ![](../img/types/vec3.png) | **Scale** | Scale of the joint. The socket label reflects the current **Space** value. |


## Properties


| Joint | The joint whose transform is read. Pick a joint from the skeleton of the mesh assigned to the graph. |
|---|---|
| Space | Coordinate space in which the transform is read: Local (relative to the parent joint) or Object (relative to the skeleton root). The default value is Local. |


## See Also


- [Set Joint Transform](../../../../../content/animations/graph/node_library/transform/set_joint_transform.md)
