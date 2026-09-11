# Animation Graph Editor


**Animation Graph Editor** is a visual tool for building animation graphs in UNIGINE. It provides a node canvas where you create nodes, connect their ports, and define the animation logic for your characters. The editor supports nested navigation into state machines, subgraphs, and blend spaces, a real-time animation preview, and a full undo/redo system.

   Sorry, your browser does not support embedded videos.
## Creating Your First Graph


To create a new animation graph:


1. Right-click in the **Asset Browser** and choose *Create -> Animation Graph*. This creates a new `*.agraph` file.
2. Double-click the created asset to open it in the Animation Graph Editor.


| ![](create_agraph.png) | ![](file_animation_graph.png) *An .agraph asset in the Asset Browser* |
|---|---|


## Editor Layout


The Animation Graph window is divided into the following areas:


### Toolbar


Located at the top of the window:


- **Load** - open an `*.agraph` file.
- **Save** - save the current graph. The button turns green when there are unsaved changes.
- **Save As** - save to a new `*.agraph` file.
- **Back / Forward arrows** - navigate through the graph browsing history.
- **Breadcrumb Bar** - shows the current location in the graph hierarchy. Click any segment to navigate to that level.


![](toolbar.png)


### Node Canvas


The main editing area where you create, arrange, and connect nodes. The canvas supports panning and zooming. Its contents change depending on the current navigation level - for example, inside a [Blend Space](../../../content/animations/blend_spaces/index.md) the canvas turns into a 2D grid with sample points, and inside a [State Machine](../../../content/animations/state_machines/index.md) the set of available nodes is limited to states and transitions.


![](canvas.png)


> **Notice:** Nodes that output an AnimPose display a **preview eye** icon in their header. Click it to toggle displaying this node's pose in the 3D preview viewport.
>
>
> ![](pose_preview.png)
>
>
> Vec3 and Quat nodes have their own eye icon in the header that shows the value in the preview viewport instead of a pose. This applies to the **[Vec3](../../../content/animations/graph/node_library/constant/vec3.md)** and **[Quaternion](../../../content/animations/graph/node_library/constant/quaternion.md)** constant nodes, and to parameter nodes of the same types.
>
>
> ![](vec3_preview.png)
>
>
> When enabled, the value appears in the viewport as a **point** labelled with the name of the node and its type. Click the point to open the manipulator: a **move gizmo for a Vec3**, a **rotate gizmo for a Quat**. Dragging it edits the value, which is a quick way to position something like an IK or look-at target directly in the viewport. For a *parameter* node the **change applies right away**; for a *constant node* it **takes effect after you save the graph**.


### Side Panels


A set of collapsible sections on the side of the window. Their contents change depending on the current context - for example, when editing a [subgraph](../../../content/animations/sub_graphs/index.md), the preview is replaced by **Subgraph Inputs** and **Subgraph Outputs** sections.


![](right_panel.png)


| Preview | A 3D viewport showing the animated character in real time. Use *Play / Pause* to control playback and the *Speed* slider to adjust playback speed (click the reset button to return to 1.0). To set up the preview, select a skinned mesh in the *Mesh* field under *Preview Settings*. These settings only affect the preview and do not change the animation graph or the in-game result: - *Mesh* - skinned mesh used to display animation playback. - *Fix Root Bone in Origin* - locks the root bone at the world origin. Enable this to keep the character centered when animations contain root motion. - *Show Bones* - renders skeleton bones as lines connecting each joint. - *Show Bone Axes* - displays local coordinate axes (red = X, green = Y, blue = Z) at each joint. - *Show Bone Names* - displays bone name labels next to each joint. - *Show Ground* - displays a ground plane in the preview scene. |
|---|---|
| Animation Graph Settings | Global settings that affect how the entire animation graph behaves at runtime: - *Root Motion* - enables animation-driven character movement. See [Root Motion](../../../content/animations/root_motion/index.md) for details. - *Filter by Skeleton* - when enabled, asset selection fields only show meshes and animations compatible with the skeleton assigned to this graph. |
| Parameters | Variables that control the animation graph at runtime. Create parameters here and use them as nodes in the graph. Their values can be changed from game logic via code. The panel provides controls to add, remove, reorder, and clone parameters. Preview overrides let you tweak parameter values in real time without writing code - they affect only the preview and do not modify saved defaults. An override that differs from the default is highlighted, with a *Reset to Default* button next to it. |
| Selected Item | Displays editable properties of the currently selected node or connection. |
| Graph Hierarchy | Tree view showing all nodes organized by nesting level, with a search filter. Click a node to select it, double-click to navigate inside. The hierarchy panel can be moved to the left side of the window - hover over the panel header and click the arrow button. |


## Navigation and Shortcuts


Everything you need to navigate the canvas, manage nodes, and control the preview camera.


### Mouse Controls


Use the mouse to navigate the canvas, select and move nodes, and create connections between ports.

   Sorry, your browser does not support embedded videos.
| MMB drag | Pan the canvas. |
|---|---|
| Scroll Wheel | Zoom in and out (centered on cursor position). |
| Left Click | Select a node. Hold **Shift** to add to selection, **Ctrl** to remove from selection. |
| Drag on Empty Space | Box-select multiple nodes. |
| Drag on Node | Move selected nodes. Hold **Ctrl** to snap to grid. |
| Drag from Port | Create a connection. |
| Right-click on canvas | Open the node creation menu. |
| Double-click | Navigate into a nested graph (state machine, state, subgraph, blend space). |


### Keyboard Shortcuts


Common keyboard shortcuts to speed up your workflow:

   Sorry, your browser does not support embedded videos.
| Ctrl + S | Save the current graph. |
|---|---|
| Ctrl + Z / Ctrl + Y | Undo / Redo. Graph edits go onto the editor-wide undo stack shared with the rest of UnigineEditor. |
| Ctrl + C / Ctrl + V | Copy / Paste nodes (without external connections). |
| Ctrl + D | Duplicate selected nodes in place. |
| Delete | Delete selected nodes or connections. |
| F | Focus the canvas on selected nodes. |


### Preview Viewport Controls


The preview viewport lets you inspect your animation from any angle in real time. Use these controls to orbit, pan, and fly through the scene:


| LMB drag | Orbit the camera around the focus point. |
|---|---|
| MMB drag | Pan the camera. |
| RMB drag | Rotate the camera (FPS-style). |
| Alt + RMB drag | Dolly (zoom by changing distance). |
| RMB + W / A / S / D | Move the camera forward, left, backward, right. |
| RMB + Q / E | Move the camera down / up. |
| Shift | Hold to move the camera faster. |
| Scroll wheel | Zoom in and out. |
| F | Focus the camera on the mesh. |


## Navigating Nested Graphs


Some nodes contain their own internal graphs. Double-click such a node or click the **enter arrow** icon in its header to navigate into it. The breadcrumb bar updates to reflect your current location.


![](enter_arrow.png)

*The enter arrow icon in the node header opens the internal graph*


You can navigate into:


- [**State Machine**](../../../content/animations/state_machines/index.md) - to view and edit states and transitions.
- **States and Transitions** (inside a state machine) - to edit the animation logic for each state and the conditions that trigger transitions between them.
- [**Subgraph**](../../../content/animations/sub_graphs/index.md) - to edit the reusable subgraph contents.
- [**Blend Space**](../../../content/animations/blend_spaces/index.md) - to edit blend parameters and sample points on a 2D grid.


Use the breadcrumb bar or the *Back* / *Forward* buttons to navigate between levels. The camera position and zoom level are remembered for each level.


## See Also


- [Animation Graph Overview](../../../content/animations/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [State Machines](../../../content/animations/state_machines/index.md)
- [Blend Spaces](../../../content/animations/blend_spaces/index.md)
