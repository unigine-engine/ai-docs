# Fixed-Wing Template - PathPlacer Plugin


**PathPlacer** is a **simplified template** of an Editor plugin for placing (spawning) objects along lines and splines. It is intended for quick procedural placement of repeated elements (props, markers, cables, etc.) along a defined path.


The plugin is based on two [components](../../../principles/component_system/index.md):


- *[PathPlacerSpline](#component_spline)* — defines and edits the path geometry (spline/line).
- *[PathPlacerSpawnNode](#component_spawnnode)* — defines what nodes to spawn along the path and the placement rules (spacing, offsets, mirroring, rows, etc.).


## Plugin Interface


Open the plugin window via *Tools -> PathPlacer Plugin*.


The window contains seven buttons, some of them may be inactive. Buttons become active when at least one node with the *[PathPlacerSpline](#component_spline)* component is selected. If multiple suitable nodes are selected, the action is applied to one of them randomly.


![](../modules/pathplacer/plugin_interface.jpg)


| Create Spline | Creates a *NodeDummy* with the *[PathPlacerSpline](#component_spline)* and *[PathPlacerSpawnNode](#component_spawnnode)* components assigned to it. The node is placed at the first detected object under the screen center (first hit); if there is no hit, position defaults to (0, 0, 0). After creation, the plugin automatically switches to spline edit mode. |
|---|---|
| Edit Mode | Toggles spline editing for the selected node. |
| Show All Paths | Visualizes all splines in the scene. |
| Generate Objects (Selected Paths) | Removes the selected path node’s children and spawns new objects according to the *[PathPlacerSpawnNode](#component_spawnnode)* settings. |
| Clear Objects (Selected Paths) | Removes all child nodes from the selected path node. |
| Generate Objects (All Paths) | Clears children and spawns objects for all Spline components in the scene using their corresponding *[PathPlacerSpawnNode](#component_spawnnode)* settings. |
| Clear Objects (All Paths) | Removes all child nodes from every node containing a *[PathPlacerSpline](#component_spline)* component in the scene. |


## Typical Workflow


1. [Create a spline](#create_spline).
2. Edit the path in [Edit Mode](#edit_mode): ![](../modules/pathplacer/edit_spline.gif) *Editing a spline*

  - Select a point by clicking it — it highlights and shows a transform gizmo.
  - Adjust point positions using gizmos or the *[Points](#points)* parameter in the *[PathPlacerSpline](#component_spline)* component.
  - Remove selected point: press **R**.
  - Add point: press **A**.

    - A new point is created at the cursor position.
    - The point is added to the beginning or the end of the spline, depending on which side is closer.
    - If the cursor is over the spline segment when pressing A, the point is inserted between the two nearest neighboring points.
  - For a straight line: use two points and set [Subdivisions](#subdivisions) = 0.
3. Configure the parameters of *[PathPlacerSpawnNode](#component_spawnnode)*, which is also assigned to the node created for the spline (set the node that will be spawned, define the distance between spawned instances, etc.).
4. In the PathPlacer plugin interface, click [Generate Objects (Selected Paths)](#generate_selected) or [Generate Objects (All Paths)](#generate_all).


The following example shows two Node References spawned along the same spline with slight variations in the Spawn Node parameters (different step and lateral offset values):


[![](../modules/pathplacer/two_nodes_spawned.jpg)](../modules/pathplacer/two_nodes_spawned.jpg)

*Two nodes spawned along the same spline*


> **Notice:** Assign only one *[PathPlacerSpline](#component_spline)* and one *[PathPlacerSpawnNode](#component_spawnnode)* component per node. Multiple instances may work but can produce incorrect results.


### Tips


- Nodes are spawned along the projection of the spline onto the terrain surface. They follow the terrain while preserving the source node’s transform parameters (height offset and rotation). The spline’s vertical curvature affects the vertical rotation of the spawned nodes. Therefore, it is recommended that the spline closely conforms to the terrain surface for optimal placement results. ![](../modules/pathplacer/no_elevation.jpg) *Spline with no elevation changes on an even surface* ![](../modules/pathplacer/elevation.jpg) *Spline with elevation changes on an even surface* ![](../modules/pathplacer/hills.jpg) *Spline with elevation changes on an uneven surface*
- A spline can be oriented by transforming its parent node: reset the spline transform and rotate/transform its parent. This makes it easier to operate in local coordinates and set precise values.
- To spawn only a single node (or a single row), set **[Step > (Distance - Offset From Start)](#component_spawnnode)**. This results in one placement at **[Offset From Start](#component_spawnnode)** (or a single row if row spawning is enabled).


> **Warning:** Do not remove the *[PathPlacerSpline](#component_spline)* component from a node, this may lead to a crash. Remove the entire node instead.


## Component Reference


### PathPlacerSpline


![](../modules/pathplacer/spline_component.jpg)


| Subdivisions | Number of segments used to subdivide the spline. If set to 0, the spline becomes a sequence of straight segments between points (useful for a pure polyline, but less convenient to edit smoothly). |
|---|---|
| Points | An array of control points. |


### PathPlacerSpawnNode


Defines spawning rules for a given path.


![](../modules/pathplacer/spawnnode_component.jpg)


| Start From | Defines the direction of placement: - **Begin**: from the start of the path - **End**: from the end of the path - **Both**: mirrored placement from both ends (intended for symmetrical layouts) |
|---|---|
| Spawn Nodes | An array of entries; each entry defines a node to spawn and its placement rules. |
| Spawn Node entry fields: |  |
| Name | Name assigned to spawned nodes in the scene. |
| Node | The `*.node` asset to spawn. |
| Offset From Start | Distance offset from the start point (start point depends on [Start From](#start_from)). Can be negative. |
| Lateral Offset | Offset from the path to the right (positive values) or to the left (negative values). |
| Distance | Total placement length (inclusive) starting from [Offset From Start](#offset_from_start). |
| Rotation | Additional rotation applied to spawned nodes. ![](../modules/pathplacer/rotation_0.jpg) *Rotation = 0* ![](../modules/pathplacer/rotation_90.jpg) *Rotation = 90* |
| Step | Spacing between spawned nodes along the path. |
| Mirror Horizontally | Mirrors spawned nodes horizontally. |
| Nodes in a Row | Number of nodes spawned sideways (across the path). |
| Row Step | Spacing between nodes in a row (horizontal step). |
