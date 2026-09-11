# Fixed-Wing Template - PathPlacer Plugin


**PathPlacer** is an Editor plugin for procedural object placement (spawning) along splines. It is designed for quick distribution of repeatable elements (props, markers, lights, cables, etc.) along a defined path.


![](../custom/img/spline_point_gizmo.png)


The plugin is built on two *[components](../../../principles/component_system/component_system_cpp/index.md)*:


- *[PathPlacerSpline](#component_spline)* - used to create and edit path geometry (spline).
- *[PathPlacerSpawnNode](#component_spawnnode)* - used to specify which nodes to spawn along the path and placement behavior: spacing, offsets, mirroring, rows, etc.


A *Dummy Node* with the two components assigned is automatically added to the scene when *[a new spline is created](../../../sdk/templates/fixedwing/custom.md#custom_path)*.


## Plugin Interface


To open the plugin window in the Editor, go to *Tools -> PathPlacer Plugin*.


The window contains controls for spline generation and editing, as well as buttons for deleting distributed objects. Editing and path-specific manipulation buttons are active when at least one node with the *[PathPlacerSpline](#component_spline)* component is selected.


> **Notice:** If multiple spline nodes are selected, the action applies only to the last one in the *World Nodes* hierarchy.


![](../modules/pathplacer/img/plugin_interface.png)


| Create Spline | Creates a *NodeDummy* with the *[PathPlacerSpline](#component_spline)* and *[PathPlacerSpawnNode](#component_spawnnode)* components assigned to it. The node is placed at the first detected object under the screen center (first hit); if there is no hit, position defaults to (0, 0, 0). After creation, the plugin automatically switches to spline *[Edit](#edit_mode)* mode. |
|---|---|
| Edit Mode | Toggles *spline editing* for the selected node. |
| Show All Paths | Visualizes all splines created with the *[PathPlacerSpline](#component_spline)* component in the scene. |
| Generate Objects (Selected Paths) | Removes all child nodes from the selected path node (if any) and spawns new objects according to the *[PathPlacerSpawnNode](#component_spawnnode)* settings. |
| Clear Objects (Selected Paths) | Removes all child nodes from the selected path node. |
| Generate Objects (All Paths) | Removes all child nodes from every node containing a *[PathPlacerSpline](#component_spline)* component in the scene, and spawns new objects according to the *[PathPlacerSpawnNode](#component_spawnnode)* settings. |
| Clear Objects (All Paths) | Removes all child nodes from every node containing a *[PathPlacerSpline](#component_spline)* component in the scene. |


The lower part of the plugin window provides quick tooltips that explain button functions and keyboard shortcuts while in *Edit Mode*:


![](../modules/pathplacer/img/plugin_interface_tooltips.png)


## Component Reference


### PathPlacerSpline


`PathPlacerSpline` is a property automatically assigned by the framework to the default `SPLINE_NODE` *Dummy Node* when a new spline is created. The `PathPlacerSpline` component allows you to edit splines by modifying control point coordinates and to adjust spline curvature using the following exposed parameters:


![](../modules/pathplacer/img/spline_component.jpg)


| Subdivisions | Number of segments used to subdivide the spline. If set to 0, the spline becomes a sequence of straight segments between points for linear object placement. |
|---|---|
| Points | An array of control points with a defined total count and world coordinates. |


### PathPlacerSpawnNode


`PathPlacerSpawnNode` is a property automatically assigned by the framework to the default `SPLINE_NODE` *Dummy Node* when a new spline is created. The `PathPlacerSpawnNode` component allows you to define object spawning rules for the current path using the following exposed parameters:


![](../modules/pathplacer/img/spawnnode_component.jpg)


| Start From | Defines the direction of placement: - **Begin**: from the start of the path - **End**: from the end of the path - **Both**: mirrored placement from both ends (intended for symmetrical layouts). |
|---|---|
| Spawn Nodes | An array of entries. Each entry defines a node to spawn and its placement rules. Increase the *Spawn Nodes* total count to place more than one *Node Reference* along the same spline. |
| Spawn Node entry fields: |  |
| Name | Name assigned to spawned nodes in the scene. |
| Node | The `*.node` asset to spawn. |
| Offset From Start | Distance offset from the start point (start point depends on *[Start From](#start_from)*). Can be negative. ![](../modules/pathplacer/img/start_offset.png) *Offset From Start = 3* |
| Lateral Offset | Offset from the path to the right (positive values) or to the left (negative values). ![](../modules/pathplacer/img/lateral_offset.png) *Lateral Offset = 0.7* |
| Distance | Total placement length (inclusive) starting from *[Offset From Start](#offset_from_start)*. ![](../modules/pathplacer/img/distance.png) *Distance = 3* |
| Rotation | Additional rotation applied to spawned nodes. ![](../modules/pathplacer/img/rotation_0.png) *Rotation = 0* ![](../modules/pathplacer/img/rotation_90.png) *Rotation = 90* |
| Step | Spacing between spawned nodes along the path. ![](../modules/pathplacer/img/step.png) *Step = 2.5* |
| Mirror Horizontally | Mirrors spawned nodes horizontally. ![](../modules/pathplacer/img/mirror.png) *Nodes in a Row = 2, mirrored* |
| Nodes in a Row | Number of parallel rows of nodes spawned along the spline. ![](../modules/pathplacer/img/nodes_row.png) *Nodes in a Row = 2, Row Step = 0.5* |
| Row Step | Horizontal spacing between rows. |
