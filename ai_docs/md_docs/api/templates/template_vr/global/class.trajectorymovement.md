# TrajectoryMovement Component

**Inherits from:** ComponentBase


TrajectoryMovement moves the node along a predefined path at a constant velocity. The path is defined by child nodes of the specified path node, with positions and rotations interpolated between waypoints.


The component loops along the path continuously. When debug mode is enabled, the path is visualized with helper lines.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| path_node | *Node* | Parent node containing waypoint child nodes that define the movement path. |
| velocity | *Float* | Movement speed along the path. Default: 10.0. |
| debug | *Toggle* | Enable debug visualization of the path. |
