# Blend Spaces


A blend space enables you to blend between multiple animations based on continuous input values. Instead of manually wiring **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** nodes with weights, you place animation samples as points in a 2D space and let the system automatically calculate blend weights based on the current input position.


Blend spaces are commonly used for locomotion systems - for example, blending between idle, walk forward, walk left, walk right, and walk backward animations based on the character's speed and direction.


There are two types of blend space nodes:


- **Blend Space 2D** - each point contains its own nested graph, so each point can use any combination of nodes (not only a single animation clip). Points are evaluated independently and blended by weight. ![](../graph/node_library/img/blendspace_2d.png)
- **Blend Space 2D Sync** - each point references a single animation asset with a playback speed multiplier. All animations play in sync - they share the same normalized playback position, so footsteps and other cyclic events stay aligned. This is the preferred choice for locomotion cycles. The node also supports [synchronization groups](../../../content/animations/synchronization/index.md) for syncing with other nodes outside the blend space. ![](../graph/node_library/img/blendspace_2d_sync.png)


Both types take two Float inputs (X and Y) that define the current position in the blend space and output a single blended Pose. Double-click the node to enter the blend space editor.


## Blend Space Editor


Double-click a **Blend Space 2D** or **Blend Space 2D Sync** node to enter the blend space editor. The canvas switches to a 2D grid view with labeled axes, a grid overlay, and blend points as draggable markers.


![](blend_space_preview.png)


### Managing Points


Right-click on the grid to add a new point at the cursor position. Drag points to reposition them - hold **Ctrl** while dragging to snap to the grid. Points are clamped to the axis range and cannot be placed outside the configured minimum and maximum values.


When a point is selected, its properties appear in the *Selected Item* panel:


- For **Blend Space 2D**: the point's name and position.
- For **Blend Space 2D Sync**: the point's name, position, animation asset, playback speed, and a *Show Preview* checkbox.


### Editing a Point's Nested Graph (Blend Space 2D only)


Double-click a point in a **Blend Space 2D** to navigate into its nested graph. Build the animation logic using any nodes, and route the result to the **[Output Pose](../../../content/animations/graph/node_library/output/output_pose.md)** node.


![](bs2d_point.png)

*Each point in a Blend Space 2D contains its own nested graph that outputs a pose*


### Previewing the Blend Position


Click the middle mouse button or right-click and drag on the grid to preview the blend at a specific position. A crosshair appears showing the current preview position, and the animation preview updates in real time to show the blended result.

   Sorry, your browser does not support embedded videos.
## Blend Space Settings


The following properties are available in the *Selected Item* panel when the blend space node itself is selected (click the node background, not a point):


| Axis X | Display name for the X axis (e.g., Speed, Direction). |
|---|---|
| Axis Y | Display name for the Y axis (e.g., Strafe, Angle). |
| Grid X | Number of grid cells along the X axis, for visual reference. Range: 1 to 20. |
| Grid Y | Number of grid cells along the Y axis. Range: 1 to 20. |
| Axis Min | Minimum value for both axes. Points cannot be placed below this value. |
| Axis Max | Maximum value for both axes. Points cannot be placed above this value. |
| Mode | Interpolation mode that determines how blend weights are calculated. - Cartesian - weights are based on straight-line distances in the 2D space. Points closer to the current position receive higher weights. Works well for most use cases, including linear locomotion blends (forward/backward/left/right). - Polar - weights are based on radial distance and angular difference. Treats the blend space as a polar coordinate system, where the distance from the origin and the angle around it are the two blending dimensions. Better suited for rotational animations - for example, blending between turn-left, turn-right, and no-turn arranged around the center. |
| Smooth Weights | When enabled, blend weights transition gradually over time instead of snapping instantly when the input position changes. This prevents sudden pops when the blend position moves quickly - for example, when driven by joystick input or physics-based velocity. |
| Smoothing Speed | Controls how fast the weights converge to their target values when *Smooth Weights* is enabled. Higher values mean faster convergence (more responsive but less smooth), lower values mean slower, more gradual transitions. The smoothing is frame-rate independent. |


> **Notice:** The axis range applies equally to both axes - you cannot set different ranges for X and Y independently.


## See Also


- [Animation Graph Editor](../../../content/animations/graph/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [Animation Synchronization](../../../content/animations/synchronization/index.md)
- [State Machines](../../../content/animations/state_machines/index.md)
