# Selecting and Positioning Nodes


The main functions of node's selection and positioning are available via the *Positioning* panel.


![](positioning_panel.png)


All available controls for selecting and positioning nodes can be found on the *Nodes* tab of the *[Editor Hotkeys](../../editor2/settings/hotkeys/index.md)* settings.


## Selecting Nodes


By default, selection is available for all nodes in the viewport. However, you can manage that with the **[Selection](../../editor2/node_parameters/transformation_common/index.md#selection)** ![](../organizing_nodes/selection_on.png) flag - toggle it on and off in the *[World Nodes](../../editor2/organizing_nodes/index.md)* or *[Parameters](../../editor2/node_parameters/transformation_common/index.md)* window to specify which nodes can be selected.


| ![](selection_hierarchy_window.png) | ![](selection_parameters_window.png) |
|---|---|
| *Selection Flags in World Nodes Window* | *Selection Flag in Parameters Window* |


To **select a single node** in the scene, choose ![](icons/select.png) on the *Positioning* panel (or press **Q**) and click the left mouse button on this node. In this case, only the mesh surface you have clicked is selected. To select several mesh surfaces, hold **Shift** and click required surfaces.


> **Notice:** You can convert the selected node to a *[NodeReference](../../objects/nodes/reference/index.md)* by pressing **Ctrl+Shift+G** (or click *Edit -> Convert to NodeReference*).


To **select several nodes**, do either of the following:


- Use the *selection box*: click and hold the left mouse button, drag the mouse to select the required nodes. In this case, all surfaces of each mesh (if they exist) are selected. ![](select_box.gif) *Select usingSelection Box*
- Select one of the nodes, press and hold **Shift** to add nodes to the selection and **Ctrl** to remove. ![](select_shift_keys.gif) *Add and remove nodes from selection*


> **Notice:** To select all nodes in the world, press **Ctrl+A**.


The viewport window has the ***Selection Filter*** dropdown that allows defining which types of objects are to be selected by a selection frame and if icons should be used instead bounds for selection (the ***Use Icons For Frame Selection*** option).


![Selection Filter](selection_filters.png)


When the node is selected, the following is shown:


- Wireframe of the node
- Bounding box of the node
- Bounding box of the selected surface (or surfaces)


The total number of currently selected nodes is displayed in the *Parameters* window.


![](selected_nodes.png)


To **remove nodes from the selection (deselect)**, press and hold **Ctrl** and click the left mouse button on the required nodes.


To **deselect** all selected nodes, press **Esc** or **Ctrl+Shift+A**.


The selected nodes can be positioned in the world by using one of the ways described [below](#move_object).


> **Notice:** You can set a *[pivot point](#pivot_point)* relative to which the selected nodes will be transformed.


### Inverse Selection


Inverse selection can be useful for complex selections. For example, if you need to select all objects in a scene except the specific ones, you can select these specific objects and invert the selection.


To invert the current selection, press **Ctrl+I**.


## Moving, Rotating and Scaling Nodes


To transform nodes, choose the required transformation mode (manipulator) on the *Positioning* panel of the **Toolbar**.


> **Notice:** You can specify the position, rotation, and scale in the *[Parameters](../../editor2/node_parameters/transformation_common/index.md)* window.


By default, any node in the world can be transformed. However, you can toggle transformations of specific nodes on and off using the **Transformation** ![](../organizing_nodes/transformation_on.png) flag in the *[World Nodes](../../editor2/organizing_nodes/index.md)* or *[Parameters](../../editor2/node_parameters/transformation_common/index.md)* window.


| ![](transformation_hierarchy_window.png) | ![](transformation_parameters_window.png) |
|---|---|
| *Transformation Flags in World Nodes Window* | *Transformation Flag in Parameters Window* |


### Move Nodes


To move the node:


1. Choose the ![](icons/move_1.png) manipulator on the *Positioning* panel (or press **W**).
2. Click the required node. The axes along which the node can be moved will be shown. ![](move_object.png) *Move Node*
3. Move the node: | ![](move_arrow.png) *Move along 1 axis* | ![](move_rectangle.png) *Move by 2 axes* | ![](move_circle.png) *Move in the screen plane* | |---|---|---|

  - If the arrow manipulator is dragged, the node can be moved along the selected axis.
  - If the rectangle manipulator is dragged, the node can be moved by two axes.
  - If the circle manipulator is dragged, the node can be moved in the screen plane.


You can also move the selected node by pressing the **arrow keys**:


1. Choose the ![](icons/move_1.png) manipulator.
2. Enable snapping [by Grid](#snap_grid) and specify the movement step. Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) If snapping [by Grid](#snap_grid) is disabled, the node is moved by 1.0 unit.
3. Select the node you want to move in the viewport. Move the node using the **arrow keys**. The direction of movement is projection-dependent.


In addition, you can:


- Ignore the node's hierarchy when moving the selected node: press **Alt** and move the node without its children. ![](move_alt.gif)
- Move the selected node to the camera by pressing **Alt+X**. ![](move_alt_x.gif)


### Rotate Nodes


To rotate the node:


1. Choose the ![](icons/rotate.png) manipulator on the *Positioning* panel (or press **E**).
2. Click the required node. The sphere with the axes, around which the node can be rotated, will be shown. ![](rotate_object.png) *Rotate node*
3. Rotate the node: | ![](rotate_axes.png) *Rotate around 1 axis* | ![](rotate_sphere.png) *Rotate freely* | |---|---|

  - If an axis of the sphere is dragged, the node is rotated around the axis.
  - If the sphere is dragged, the node can be rotated freely around several axes.


You can also rotate the selected node with the given step by using the **arrow keys**:


1. Choose the ![](icons/rotate.png) manipulator.
2. Enable [snapping by angle](#snap_angle) and specify the step for the rotation angle. Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) If [snapping by angle](#snap_angle) is disabled, the node is rotated by 20 degrees.
3. Select the node you want to rotate in the viewport. Rotate the node by using the **arrow keys**. The direction of rotation is projection-dependent.


### Scale Nodes


To scale the node:


1. Choose the ![](icons/scale.png) manipulator on the *Positioning* panel (or press **R**).
2. Click the required node. The axes, along which the node can be scaled, will be shown. ![](scale_object.png) *Scale Node*
3. Scale the node: | ![](scale_axis.png) *Scale along 1 axis* | ![](scale_square.png) *Scale along 2 axes* | ![](scale_triangle.png) *Scale along 3 axes* | |---|---|---|

  - If the red, green, or blue cube manipulator located at the end of any axis is dragged, the node is scaled along this axis.
  - If the red, green, or blue square manipulator is dragged, the node is scaled along two axes.
  - If the white cube manipulator at the origin is dragged, the node is scaled along three axes.


It is also possible to scale the selected node with the given step by using the **arrow keys**:


1. Choose the ![](icons/scale.png) manipulator.
2. Enable [snapping by scale](#snap_scale) and specify the step. Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) If [snapping by scale](#snap_scale) is disabled, the node is scaled by 0.1 unit.
3. Select the node you want to scale in the viewport. Scale the node using the **arrow keys**. The direction of scaling is projection-dependent.


## Clone and Delete Nodes


To **clone** a node:


1. [Select](#select_nodes) the node.
2. Press **Ctrl+D** (or *Edit -> Clone*). > **Notice:** The cloned node will have the same position as the source node.


To **clone and transform** a node:


1. [Select](#select_nodes) the node.
2. Choose ![](icons/move_1.png), ![](icons/rotate.png), or ![](icons/scale.png) on the *Positioning* panel (or press **W, E**, or **R**).
3. Press and hold **Shift** and transform the node.
4. Press **Shift + D** as many times as required (or press and hold this combination) to create more clones. Every next clone will use the last applied transformation.


![](clone_prev_transform.gif)


To **clone a node with snapping and manual positioning**:


1. Enable snapping **[by Grid](#snap_grid)** and set the required step value. Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif)
2. Select an object to be cloned in the world.
3. Choose the **[Move](#move_object)** manipulator.
4. Press and hold **Shift + Alt** while dragging an object with the mouse or using arrows on the keyboard. A new clone is created every step.


![](multiple_clone_manual.gif)


You can also clone the node holding **Shift** and using the **arrow keys**. The direction of cloning is projection-dependent:


![](clone_move.gif)


To **delete** a node, select it and press **Delete** (or click *Edit -> Delete Object*).


## Pivot Point and Coordinate System


Transformations of the node are relative to the pivot point. The *pivot point* is used to control the way nodes rotate and scale.


To rotate or scale several nodes, select them, choose the required [manipulator](#transform_objects), and specify the position of its pivot point by using the *pivot point toggle*.


> **Notice:** If one node is selected, the pivot point position will not change when toggling.


- If the ![](icons/center.png) button is active, the pivot point is set to the center of selection.
- If the ![](icons/pivot.png) button is active, the pivot point is set to the center of the last selected node.


> **Notice:** To toggle the pivot point, you can press **Z**.


For example:


- If you select several nodes, set the pivot point toggle to *Center*, and rotate these nodes, they rotate around the center of selection as follows: ![](rotate_center.gif) *Pivot point in the center of selection* > **Notice:** If you scale the nodes, they are scaled out from or in toward the center of selection.
- If you set the pivot point toggle to *Pivot* and rotate the selected nodes, each node will rotate around its center as follows: ![](rotate_pivot.gif) *Pivot point coincides with the center of the last selected node* > **Notice:** If you scale nodes, each node is scaled relative to its center.


The *basis* of the manipulator pivot point can be toggled as follows:


- If the ![](icons/world_1.png) button is active, the world space orientation is used for the manipulator pivot point. For example, if you set the ![](icons/pivot.png) ![](icons/world_1.png) combination for the selected nodes and rotate them around the Y axis, you will get the following: | Before rotation: | After rotation: | |---|---| | ![](pivot_world.png) | ![](pivot_world_rotate.png) | | *Pivot point is oriented by the world space* | *Nodes have been rotated by 45 degrees around the Y axis* |
- If the ![](icons/parent.png) button is active, the coordinate system of the parent node is used for the pivot point orientation. For example, if you set the ![](icons/pivot.png) ![](icons/parent.png) combination for the selected nodes and rotate them around the Y axis, you will get the following: | Before rotation: | After rotation: | |---|---| | ![](pivot_parent.png) | ![](pivot_parent_rotate.png) | | *Pivot point is oriented by the local basis of the parentnode (the red cube)* | *Nodes have been rotated by 45 degrees around the Y axis* |
- If the ![](icons/local.png) button is active, the pivot point is oriented by the local coordinate system of the node. It means that its orientation does not depend on the parent node orientation. For example, if you set the ![](icons/pivot.png) ![](icons/local.png) combination for the selected nodes and rotate them around the Y axis, you will get the following: | Before rotation: | After rotation: | |---|---| | ![](pivot_local.png) | ![](pivot_local_rotate.png) | | *The pivot point is oriented by the local basis of the lastselected node (the green cube)* | *The nodes have been rotated by 45 degrees around the Y axis* |


> **Notice:** To toggle the manipulator basis, you can press **Z**.


## Manipulations Snapping


To perform positioning, rotation, and scaling manipulations with a higher precision, the *Positioning* panel provides tools that allow defining a manipulation step.


### Position Snapping by Grid


**Snap by Grid** enables to position a node along the axis or over the grid with a given arbitrary *step* (**By Grid**) or with a step equal to the dimensions of node's bounding box (**By Bound Box**).


> **Notice:** Snapping should be enabled when moving the node by using [arrow keys](#move_with_arrows). If disabled, the node is moved by 1 unit by default.


To snap a node **by Grid**:


1. Choose ![](icons/snap_grid.png) on the *Positioning* panel (or press **W**).
2. Choose **By Grid** and specify the grid *step* (in units) using the drop-down box: ![](icons/snap_step.png) Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) Now you can move any node in the world along an axis or across a grid with the given step.
3. [Move](#move_object) one of the nodes: | ![](pos_axis.jpg) *Snapping by an axis* | ![](pos_grid.jpg) *Snapping by a grid stripes* | |---|---|

  - If one axis is chosen (the arrow manipulator is dragged), the node is aligned along the axis.
  - If a node is repositioned by two axes (the rectangle manipulator is dragged), the node will be aligned by a horizontal or vertical grid.


### Position Snapping by Bound Box


To snap a node **by Bounding Box**:


1. Choose ![](icons/snap_grid.png) on the *Positioning* panel (or press **W**)
2. Choose **By Bound Box** using the drop-down box: ![](icons/snap_step.png) Now you can move any node in the world along an axis or across a grid with the step equal to the size of the node.
3. [Move](#move_object) one of the nodes: ![](bb_snapping.gif)

  - If one axis is chosen (the arrow manipulator is dragged), the node is aligned along the axis.
  - If a node is repositioned by two axes (the rectangle manipulator is dragged), the node will be aligned by a horizontal or vertical grid.


### Position Snapping by Vertex


**Vertex snapping** allows you to position objects in the world relative to others so that the desired vertices meet precisely, preventing gaps or overlaps.


This tool helps you quickly assemble scenes by snapping together modular objects (e.g., pipes or building segments), walls, interior and exterior elements, power lines, and other assets that usually require fine manual alignment (e.g., to match simplified geometry with an existing high-poly model).


To snap a node **by Vertex**:


1. Press **W** to enable **Move node** mode or choose ![](icons/move_1.png) on the *Positioning* panel.
2. Press **Shift+Z**, select **By Vertex** from the drop-down, or hold **V** to snap on demand. ![](icons/snap_by_vertex.png) The *Distance* parameter defines how far selectable pivot vertices of the manipulated mesh can be from the camera. All visible vertices of another mesh will be considered snap targets if the closest vertex of this mesh is within the specified range. This helps prevent snapping to distant or irrelevant geometry. If necessary, adjust the *Distance* (50 units by default) manually or use the box as a slider. ![](snap_by_vertex_slider.gif) When you hover the cursor over a vertex of the **selected** object, all of the object's vertices are outlined with a mesh grid. ![](snap_by_vertex_grid.png)
3. Choose the pivot vertex for your object and move the cursor over it for the vertex snapping manipulator to appear. Hold **LMB** and drag the vertex circle manipulator toward another object's vertex. Release **LMB** (and **V**, if held) when the object is positioned correctly. ![](snap_by_vertex.gif) You can also move the node vertex along **one or two particular axes** - when the vertex manipulator appears, select an axis to constrain the snapping direction and drag the arrow or rectangle manipulator respectively. ![](snap_by_vertex_axes.png) To snap the pivot vertex to **occluded vertices**, enable ***X-Ray Snapping*** mode. In this mode, if the pivot vertex is dragged in front of a hidden object, an auxiliary mesh grid visualizes the occluded vertices, allowing you to snap to them. ![](snap_by_vertex_xray.png)


**Vertex snapping is supported for**:


- **Vertex-to-vertex** for *Mesh Static* and *Mesh Dynamic* objects
- **Pivot-to-vertex** for other mesh types (*Mesh Skinned, Mesh Decal*, etc.)
- **Mesh Cluster** objects in the **Edit** mode
- **Mesh** objects stored in a **Node Reference**.


> **Warning:** Vertex snapping may slow down the Editor's performance in complex scenes.


Watch the quick video guide on positioning objects using Vertex Snapping:


### Rotation Snapping by Angle


**Snap by Angle** allows rotating a node along the axis with a given *step* (in degrees).


> **Notice:** Snapping should be enabled when rotating the node by using [arrow keys](#rotate_with_arrows).


To snap a node by angle:


1. Choose ![](icons/snap_angle.png) on the *Positioning* panel (or press **E**).
2. Specify the *step* for the rotation angle using the following drop-down box: ![](icons/snap_angle_step.png) Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) Now you can rotate any node in the world around the axis with the given step.
3. [Rotate](#rotate_object) the node. ![](snap_rotation.jpg) *Rotation by 45 degrees*


### Snapping by Scale


**Snap by Scale** allows scaling a node along the axis with a given *step*.


> **Notice:** Snapping should be enabled when scaling the node by using [arrow keys](#scale_with_arrows).


To snap a node by scale:


1. Choose ![](icons/snap_scale.png) on the *Positioning* panel.
2. Specify the *step* for the scale factor using the following drop-down box: ![](icons/snap_scale_panel.png) Step can be set either by direct input of digits or using the box as a slider. ![](step_size.gif) Now you can scale any node in the world along the axis with the given step.
3. [Scale](#scale_object) the node. ![](snap_scale.png) *Scaling by step 0.5*


> **Notice:** You can use the **Ctrl** button to invert snapping controls (Grid, Angle, and Scale).


## Snapping Nodes to Surface


Snapping a node to a surface of another node provides pixel-perfect positioning of the nodes relative to each other.


To snap a node to the surface:


1. [Select](#select_nodes) a node that should be snapped.
2. Choose ![](icons/snap_surface.png) on the *Positioning* panel (or press **Alt+W**).
3. Specify snapping settings via the following panel: ![](snap_surface.png) | Option | Description | |---|---| | **Offset from Surface** | Specifies the distance from the node's [pivot point](#pivot_point) to the surface (in units). > **Notice:** - To increase/decrease the distance to the surface, use the **WHEEL UP/WHEEL DOWN** hotkeys. > - To reset the distance to the surface, use the **MIDDLE CLICK** hotkey. | | **Orient by Normal** | Specifies whether the node should be oriented by the surface normal. > **Notice:** The hotkey is **RIGHT MOUSE BUTTON**. | | **Take Intersection Into Account** | If enabled, the node interacts only with the surfaces that have the *[Intersection](../../editor2/node_parameters/physics/index.md#surface_intersection)* option enabled. |
4. Move the node until the red stripe intersects the required surface of the other node. Click the left mouse button to place the node. > **Notice:** To abort placement, press **ESC**.


The node will follow the mouse as on the image below:


![](snap_to_surface.gif)


| ![](snap_surface_1.png) *Node is oriented by normal* | ![](snap_surface_2.png) *Node is not oriented by normal* |
|---|---|


## Dropping Nodes to Ground


Dropping a node to the ground means positioning a selected node to the surface below or above this node.


To drop a node to the surface:


1. [Select](#select_nodes) a node (or several nodes) that should be dropped.
2. On the *Positioning* panel, find ![](drop_to_ground.png) and specify the required settings in the drop-down window: ![](drop_panel.png) | Option | Description | |---|---| | **Direction** | Specifies the direction of dropping: - **Up** � find the closest surface above the object. - **Down** � find the closest surface below the object. - **Up And Down** � find the closest surface below the object and above it. | | **Offset from Surface** | Specifies the distance from the node's [pivot point](#pivot_point) to the surface (in units). | | **Orient by Normal** | Specifies whether the node should be oriented by the surface normal. | | **Intersection Mask** | Sets an [intersection mask](../../principles/bit_masking/index.md#intersection_mask) that defines whether a node (or nodes) will be positioned on a surface to which it is dropped. A node will be positioned on a surface if they both have matching intersection masks. Otherwise, the node will penetrate the surface. | | **Take Intersection Into Account** | If enabled, the node interacts only with the surfaces that have the *[Intersection](../../editor2/node_parameters/physics/index.md#surface_intersection)* option enabled. |
3. Click ![](drop_to_ground.png) to drop a node (nodes). | ![](drop_1.png) | ![](drop_2.png) | |---|---| | *Initial position of a node* | *Node dropped to surface (default settings)* |


## Switching between Node References


You can quickly replace the source node of *[Node Reference](../../objects/nodes/reference/index.md)* with another one stored in the same folder. To do that, select a *Node Reference* in the *World Nodes* hierarchy window or the Viewport, hold **Shift** and use the mouse wheel or the **Page Up** and **Page Down** buttons.


![](../../objects/nodes/reference/node_ref_switch.gif)
