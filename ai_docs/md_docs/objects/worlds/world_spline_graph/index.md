# World Spline Graph


> **Warning:** This feature is an experimental one and is not recommended for production use.


![](road_tool.gif)


**World spline graph** is a convenient and performance-friendly method to place specified nodes (called **source nodes**) along a spline graph (its vertices and edges). It is not a single-purpose tool designed just to create roads. It can also be used for ropes, chains, pipes, and any objects, having a form that follows a curved path. It is designed to help artists quickly build various complex structures from typical basic elements placed along spatial curves, such as pipes and tubes at an oil refinery, for example.


![](applications.png)

*World Spline Graph Applications*


> **Notice:** The use of World Spline Graph implies the object placement and deformation and a subsequent export to `.mesh` and `.fbx` files.


A spline graph is determined by a set of points **p0, p1, ... pn** and a set of edges or segments (cubic Bezier splines), that connect some or all of these points.


![](../../../code/formats/spline.png)


Each **segment** is determined by a starting (**pSTART**) and an ending (**pEND**) point, as well as **tangent** vector coordinates at these points, which determine the curvature of the segment (**tSTART** and **tEND** respectively). Points, that are shared by more than two segments are called [**junctions**](#junction).


**Source nodes** (currently *[Static Mesh](../../../objects/objects/mesh/index.md), [Skinned Mesh (Legacy)](../../../objects/objects/mesh_skinned_legacy/index.md)*, and *[Projected Decal](../../../objects/decals/proj/index.md)*) can be placed at points and along the segments of the spline graph. Each point and segment can have a single or a set of source nodes assigned. One of the following modes can be selected for each individual source node assigned to a segment:


- **stretching** - source nodes are stretched along the spline segment. > **Notice:** Stretching is available only for [Static Mesh](../../../objects/objects/mesh/index.md) source nodes.
- **tiling** - source nodes are duplicated along the spline segment.
- **adaptive** (a combination of the first two) - source nodes are duplicated along the spline segment, but the length of each node (stretching) is determined by the curvature of the corresponding part of the segment. Thus, long nodes are placed along the straight parts of segments, while short ones - along the curved parts, providing a reasonable balance between the plausible look and performance.


For example, a segment can have two source nodes assigned: one representing the road (stretched) and another for roadway lights (tiled with a [gap](#segment_gap)).


> **Notice:** Source nodes to be assigned to segments and points are stored in `*.node` files. The `*.node` file should contain a *[Static Mesh](../../../objects/objects/mesh/index.md), [Skinned Mesh (Legacy)](../../../objects/objects/mesh_skinned_legacy/index.md)*, or *[Projected Decal](../../../objects/decals/proj/index.md)* as a root node.


An arbitrary number of *WorldSplineGraph* nodes can be added to the scene as it uses a number of optimizations (such as baking elements into large segments etc.) to ensure acceptable performance for large areas.


Coordinates of the ***UP* vector** are additionally stored for each point of the segment. This vector is used to define orientation of nodes placed along the segments of the spline graph. By default this vector is parallel to the **Z** axis. The *UP* vector does not affect the curvature of the spline segment itself.


![](wsg_up_vector_adjustment.gif)

*UPvector adjustment.*


SDK includes the **Road Tool Constructor** add-on with a set of ready-to-use assets (road segments and various types of junctions) that can be used as construction elements to simplify roads creation.


> **Notice:** *WorldSplineGraph* node currently has the following restrictions:
> - it cannot be converted to a *[Node Reference](../../../objects/nodes/reference/index.md)*.
> - it is not supported by *[Node Layers](../../../objects/nodes/layer/index.md)*.


### See also


- The *[WorldSplineGraph](../../../api/library/worlds/class.worldsplinegraph_cpp.md)* class article to learn how to manage world spline graphs via API
- The *[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)* class article to learn how to manage spline graph points via API
- The *[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)* class article to learn how to manage spline graph segments via API
- C++ sample for the *WorldSplineGraph* class illustrating how to manage spline graphs and generate geometry along the graph segments: **source/samples/Api/Nodes/WorldSplineGraph**
- Samples illustrating [use cases of the *WorldSplineGraph*](../../../content/samples/main_samples/world_spline_graph.md) node included in the **[Samples](../../../content/samples/index.md)** suite:

  - `world_spline_graph/roads` - roads created on the terrain surface
  - `world_spline_graph/ropes` - ropes, chains, and cables


## Creating a World Spline Graph


To create a new *World Spline Graph*, do the following:


1. Add a *World Spline Graph* node: on the [Menu Bar](../../../editor2/interface/index.md#menu_bar), choose *Create -> Spline Graph*. ![](add_world_spline_graph.png)
2. Specify a name of existing spline file (`*.spl`) to be used for the new *World Spline Graph* or a new name to create your spline from scratch. ![](save_spline_graph.png) > **Notice:** Remember, `*.world` files store only *WorldSplineGraph* node's data (transformation, list of source nodes, etc.), while spline graphs themselves are stored in separate `*.spl` files. To save the spline graph that you created in the world, click **Save Spline** in the *Parameters* tab and specify a file name for it.
3. Edit the spline graph by managing its [points](#manage_points) and [segments](#manage_segments).
4. [Assign](#nodes_manage) desired source nodes to points and segments of the spline graph.


## Managing Points


### Adding a New Point


New points are added to the spline graph by cloninng existing ones. To add a new point do the following:


1. Select the *World Spline Graph*.
2. Select the desired point, which you wish to clone (**Move** manipulator will appear).
3. Press *Ctrl + D* on the keyboard (a new point will be created).
4. Use the **Move** manipulator to position you new created point.


![](wsg_point_create.gif)


### Adjusting Point's Position


To adjust position of a point do the following:


1. Select the *World Spline Graph*.
2. Select the desired point (**Move** manipulator will appear).
3. Use the **Move** manipulator as you would do to move a node.


![](wsg_point_adjustment.gif)


You can also adjust the position of the selected point via the *Spline Points* section of the *Parameters* tab:


![](point_position.png)


### Adjusting Point's Tangent


Tangents control the curvature of the spline segment. To adjust tangent at a point do the following:


1. Select the *World Spline Graph*.
2. Select the desired point (**Move** manipulator will appear).
3. Select the desired tangent (in case the selected point is shared by multiple segments, several tangents will be displayed for it). As you select a tangent the **Move** manipulator appears next to it.
4. Use the **Move** manipulator as you would do to move a node (the form of the corresponding segment will change).


![](wsg_tangent_adjustment.gif)


### Adjusting Point's UP Vector


Up vector controls orientation of nodes placed along the spline segment. To adjust tangent at a point do the following:


1. Select the *World Spline Graph*.
2. Select the desired point (**Move** manipulator will appear).
3. Select the desired *UP* vector (in case the selected point is shared by multiple segments, several *UP* vectors will be displayed for it).
4. Switch to **Rotate** manipulator and use it to adjust the desired angle as you would do to rotate a node (the orientation of nodes placed along the corresponding segment will change). > **Notice:** You'll be able to see the effect only when a node is assigned to the corresponding segment.
5. Use the **Move** manipulator as you would do to move a node (the form of the corresponding segment will change).


![](wsg_up_vector_adjustment.gif)


### Merging Points


Sometimes it might be necessary to merge certain points (e.g. to close a spline). To merge two or more points into one do the following:


1. Select the *World Spline Graph*.
2. Select points you want to merge with a region selection tool or one-by-one while holding the *Shift* key pressed.
3. Right-click on a point you want to merge selected ones into and choose **Merge To This Point**.
4. All points will be merged into one shared by the segments, to which the merged points belonged.


![](wsg_merge_points.gif)


### Deleting a Point


To delete point(s) of the spline graph do the following:


1. Select the *World Spline Graph*.
2. Select point(s) you want to delete with a region selection tool or one-by-one while holding the *Shift* key pressed.
3. Press the *Del* key.


> **Notice:** Deleting points will automatically delete all segments, to which these points belong.


![](wsg_point_delete.gif)


## Managing Segments


### Adding a New Segment


To add a new segment to the spline graph do the following:


1. Select the *World Spline Graph*.
2. Select the starting point for the new segment to be added (**Move** manipulator will appear).
3. Press and hold the *Shift* key and use the **Move** manipulator to position the ending point of the new segment. > **Notice:** - To create a straight segment, you should drag the manipulator in the direction of the tangent at the starting point. > - The new added segment uses all settings (assigned nodes, placement modes and parameters) of the previous one.


![](wsg_add_segment.gif)


You can also clone segment(s) by selecting them and moving with the **Shift** key pressed, or pressing *Ctrl + D* and placing the clone with the **Move** manipulator.


### Deleting a Segment


To delete segment(s) of the spline graph do the following:


1. Select the *World Spline Graph*.
2. Select segment(s) you want to delete with a region selection tool or one-by-one while holding the *Shift* key pressed.
3. Press the *Del* key.


> **Notice:** If you delete a segment that enters into a junction, the latter will cease to function properly.


![](wsg_segment_delete.gif)


## Managing Source Nodes


As described above, a single or a set of [source nodes](#source_node) can be assigned to each point or segment of the spline graph.


### Workflow for Segments


To assign a source node to selected segment(s) do the following:


- Select the desired segments(s).
- Click **Add Node** in the *Parameters* tab.
- In the window that opens, select the required node and click **OK**. > **Notice:** Source nodes to be assigned to segments and points are stored in `*.node` files. The node file should contain a *[Static Mesh](../../../objects/objects/mesh/index.md), [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md)*, or *[Projected Decal](../../../objects/decals/proj/index.md)* as a root node.


For each of the source nodes assigned to the selected segment(s) the following settings are available for adjustment via the *Parameters* tab:


![](segment_node_params.png)


| Node | Path to a `*.node` file containing a source node. |
|---|---|
| Forward Axis | Defines which axis of the source node is to be oriented along the spline. |
| Placement Mode | Type of objects to be generated. One of the following: - **Stretch** - a single source node instance is stretched along the segment. > **Notice:** This mode is the most performance-friendly. - **Tiling** - multiple instances of the source node are placed along the segment. The number of instances is determined by the sizes of the segment and the source node and the value of the **[Gap](#segment_gap)** parameter. - **Adaptive** - a combination of the previous two resulting in multiple instances of the source node placed along the segment. Some of these instances may be stretched depending on segment's curvature. |
| Adaptive Threshold | Determines how much a source node's instance can be stretched in the **[Adaptive](#segment_placement_mode)** placement mode to cover the whole length of the segment. > **Notice:** Available for **Adaptive** placement mode only. |
| UV Tiling | Enables tiling of the source node's textures. |
| Gap | Defines the gap (in units) between the adjacent instances on the source node for the **[Tiling](#segment_placement_mode)** placement mode. > **Notice:** Available for **Tiling** placement mode only. |


### Workflow for Points


To assign a source node to selected point(s) do the following:


- Select the desired point(s).
- Click **Add Node** in the *Parameters* tab.
- In the window that opens, select the required node and click **OK**. > **Notice:** For a [junction](#junction) point to behave properly an *[ObjectMeshSkinned](../../../objects/objects/mesh_skinned_legacy/index.md)* node should be assigned, and the number of its bones should correspond to the number of spline segments connected to this point.


For each of the source nodes assigned to the selected point(s) the following settings are available for adjustment via the *Parameters* tab:


![](point_node_params.png)


| Node | Path to a `*.node` file containing a source node. |
|---|---|
| Variant | There is a number of possible variants for a [junction](#junction). This slider enables you to choose the one that fits best. > **Notice:** This parameter affects only the source nodes representing junctions (*ObjectMeshSkinned*). ![](point_junction_variant.gif) |


#### Junctions


Junctions should interact with all entering segments properly providing seamless transitions. For this puprose *[ObjectMeshSkinned](../../../objects/objects/mesh_skinned_legacy/index.md)* source nodes are used.


![](point_junction.gif)


Source nodes to be used for junctions must comply with the following requirements:


- Joints of a junction in the UnigineEditor must have their **Y** axes oriented from the center of the junction to the edges of the corresponding branches.
- Outer joint of each junction�s branch must be placed exactly at the center of its outer edge, weights for outer vertices of the branch must be maximal for the outer joint (i.e., outer vertices of the branch are affected only by the outer joint).
- As junction and segment are represented by separate meshes, textures and their UV maps must ensure seamless junction-segment and segment-segment transitions.
- A segment may have junctions at both of its endpoints, Therefore the texture used for the segment must be symmetrical, at least its edges.
- Specific requirements for roads:

  - A junction as well as a road segment must be represented by a pair of meshes (embankment and the road itself). Embankment mesh is used for smooth blending with terrain surface. Just enable the *Terrain Lerp* state for the material assigned to embankment.
  - To ensure correct deformation of segments and junctions triangulation for the road and embankment must match. This prevents penetration of meshes into each other when moving spline points up and down.


![](junctions.png)


## Exporting World Spline Graph


*World Spline Graph* works well as a tool for object placement and deformation, but due to some technical issues, it is difficult to use it in final applications as the resulting object. Therefore, as soon as the object arrangement is final, it is required to export the spline graph to the `.mesh` or `.fbx` file.


To export *World Spline Graph*, right-click it in the *World Nodes* hierarchy, select **Export to** and a preferable option:


- [UNIGINE Mesh file (.mesh)](../../../editor2/exporting_nodes/index.md#export_to_mesh)
- [FBX](../../../editor2/exporting_nodes/index.md#export_to_fbx)


![World Spline Graph Export](wsg_export.png)


The export operation produces unique geometry that you can use in your projects like any other model without any additional restrictions.


### Limitations


Due to the nature of the mesh, there will be visual artifacts connected with the float precision, if *World Spline Graph* is exported to a very big object (around 10,000 m from the origin to either side). We recommend splitting such big objects to smaller ones.


A problem may also arise if *World Spline Graph*, though being not very big, is located very far from the origin (around 10,000 m and further). In this case we advise exporting it to *FBX* without storing pivot (the **[Save root transform](../../../editor2/exporting_nodes/index.md#save_root_transform)** option should be disabled), or resetting the *World Spline Graph* position to origin before exporting it to *Mesh*.
