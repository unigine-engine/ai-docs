# Unigine.WorldSplineGraph Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


> **Warning:** This feature is an experimental one and is not recommended for production use.


This class is used to generate specified nodes (called **source nodes**) along a [spline graph](../../../objects/worlds/world_spline_graph/index.md).


UNIGINE's 3D spline system has a wide range of applications, particularly procedural content generation (rivers, roads, pipelines etc.).


![](../../../code/formats/spline.png)


A spline graph is determined by a set of [points](../../../api/library/worlds/class.splinepoint_usc.md) **p0, p 1, ... p n** and a set of segments (cubic Bezier splines), that connect some or all of these points.


Each [**segment**](../../../api/library/worlds/class.splinesegment_usc.md) is determined by the indices of the starting (**pSTART**) and ending (**pEND**) points and tangent vector coordinates at these points, which determine the form of the segment (**tSTART** and **tEND** respectively).


Coordinates of the **"up" vector** are additionally stored for each point of the segment. You can specify this vector to define orientation of geometry or objects, that can be [stretched or tiled along the segments](#intro) of the spline graph. By default this vector is parallel to the **Z** axis. The "up" vector does not affect the form of the spline segment.


It is possible to obtain an interpolated value for any point belonging to a segment, this can be used for various purposes (e.g. to change road profile). Interpolated "up" vector can be calculated as follows (pseudocode):


```cpp
vec3 lerpUpVector(vec3 start_up, vec3 end_up, float t) const
{
	float angle = acos(dot(start_up, end_up)) * RAD2DEG;
	vec3 rotation_axis = cross(start_up, end_up);

	return rotateAxisAngle(rotation_axis, angle * t) * start_up;
}

```


A world spline graph consists of segments and has a list of source nodes (currently [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_usc.md), [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md), and [DecalProj](../../../api/library/decals/class.decalproj_usc.md)) that can be placed at points and along the segments of the spline graph. Each point and segment can have a single or a set of source nodes assigned. An arbitrary number of WorldSplineGraph nodes can be added to the scene.


WorldSplineGraph has the following features:


- Points of the spline graph are managed via the [SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md) class.
- Segments of the spline graph are managed via the [SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md) class.
- 3 modes are supported:

  - **stretching**: source nodes are stretched along the spline segment.
  - **tiling**: source nodes are duplicated along the spline segment.
  - **adaptive** - represents a combination of the first two: source nodes are duplicated along the spline segment, but the length of each node (stretching) is determined by the curvature of the corresponding part of the segment. Thus, long nodes are placed along the straight parts of segments, while short ones - along the curved parts, providing a reasonable balance between the plausible look and performance.
- Forward axis selection for stretching/tiling source nodes.


### See Also


- Article on the [World Spline Graph](../../../objects/worlds/world_spline_graph/index.md) object
- C++ sample
- UnigineScript samples:

  -
  -


## WorldSplineGraph Class

### Members

## int getNumSplineSegments () const

Returns the current total number of [spline segments](../../../api/library/worlds/class.splinesegment_usc.md) in the world spline graph.
### Return value

Current number of segments in the world spline graph.
## int getNumSplinePoints () const

Returns the current total number of [spline points](../../../api/library/worlds/class.splinepoint_usc.md) in the world spline graph.
### Return value

Current number of spline points.
## isCurved () const

Returns the current value indicating if the world spline graph is curved.
### Return value

Current the world spline graph is curved
## getEventRebuildingFinished () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventSegmentRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventSegmentChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventSegmentAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventPointRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventPointChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventPointAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static WorldSplineGraph ( )

Default constructor. Creates an empty world spline graph.
## static WorldSplineGraph ( string name )

Constructor. Creates an empty world spline graph with a given name.
### Arguments

- *string* **name** - World spline graph name.

## void setSplineGraphName ( string name , int force_load = 0 )

Sets the name of the world spline graph.
### Arguments

- *string* **name** - World spline graph name.
- *int* **force_load** - **1** to load the world spline graph immediately from a file, **0** to update only the world spline graph name.

## string getSplineGraphName ( )

Returns the name of the world spline graph.
### Return value

World spline graph name.
## void loadSegmentNodes ( int segment_index = -1 )

Loads source nodes assigned to the specified spline segment immediately.
### Arguments

- *int* **segment_index** - Segment index. If no segment index is specified, the method loads source nodes assigned to all segments.

## void clear ( )

Clears the world spline graph.
## void makeCurved ( )


Curves the world spline graph using its geodetic pivot. The spline file is saved upon completion of the curving operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_usc.md) node.


## void makeFlat ( )


Flattens the world spline graph using its geodetic pivot. The spline file is saved upon completion of the flattening operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_usc.md) node.


## int load ( string name )

Loads a spline graph from the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to load the spline graph from.

### Return value

**1** if the spline graph was successfully loaded; otherwise, **0**.
## int save ( string name )

Saves a spline graph to the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to save the spline graph to.

### Return value

**1** if the spline graph was successfully saved; otherwise, **0**.
## static int type ( )

Returns the type of the node.
### Return value

[WorldSplineGraph](../../../api/library/nodes/class.node_usc.md#WORLD_SPLINE_GRAPH) type identifier.
## void getSegmentNodeMesh ( Mesh mesh , SplineSegment segment , int node_index , int bake_transform = 0 )

Gets a mesh used by a node with the specified index, placed along the specified [spline segment](../../../api/library/worlds/class.splinesegment_usc.md), and puts it to the specified target [Mesh](../../../api/library/rendering/class.mesh_usc.md) instance.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Target mesh instance to which the obtained mesh is to be put.
- *[SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md)* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_usc.md) for which the mesh is to be returned.
- *int* **node_index** - Number of the node instance placed along the spline segment.
- *int* **bake_transform** - **1** to use baked mesh transformation, **0** - to use default (the mesh will be placed at the origin). The default value is **0**.

## void getPointNodeMesh ( Mesh mesh , SplinePoint point , int node_index , int bake_transform = false )


Exports a mesh with the specified index placed as the specified [spline point](../../../api/library/worlds/class.splinepoint_usc.md) to the specified target mesh.


> **Notice:** Due to the nature of the mesh, there will be visual artifacts connected with the float precision, in case an exported node is located very far from the origin (around 10,000 m and further). In this case we advise exporting it without baking transformation.


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **mesh** - Target mesh to store the desired mesh placed at the specified spline point.
- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - Spline point for which a mesh is to be retrieved.
- *int* **node_index** - Number of the desired node in a row of nodes placed at the specified point, in the range from 0 to the [total number of nodes placed at the point](../../../api/library/worlds/class.splinepoint_usc.md#getNumNodes_int). > **Notice:** The node must be an [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_usc.md) or an [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md), otherwise an error occurs.
- *int* **bake_transform** -  *Bake Transform* flag: **1** - to export the mesh preserving the current coordinates (can be useful when splitting large *WorldSplineGraph* objects to keep relative positions of meshes); or **0** - to reset the position of the exported mesh to origin (0,0,0) with zero-rotation.

## SplinePoint createSplinePoint ( Vec3 position )

Creates a new [spline point](../../../api/library/worlds/class.splinepoint_usc.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *Vec3* **position** - Position coordinates for the new splint point.

### Return value

New [spline point](../../../api/library/worlds/class.splinepoint_usc.md).
## void removeSplinePoint ( SplinePoint point , int merge = 0 )


Removes the specified spline point from the world spline graph. You can set the *merge* flag to merge [spline segments](../../../api/library/worlds/class.splinesegment_usc.md) sharing this point as their start and end points.


> **Notice:** Segment merging is available only when the point to be removed is shared by two segments, otherwise the *merge* flag is ignored and all segments sharing this point are also removed.


### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) to be removed.
- *int* **merge** - **1** to merge spline segments sharing this point as their start and end points, **0** to remove all segments sharing this point. The default value is **0**.

## void getSplinePoints ( )

Returns the list of all points of the world spline graph and puts them to the specified vector of [SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md) elements.
### Arguments

## SplineSegment createSplineSegment ( SplinePoint start_point , vec3 start_tangent , vec3 start_up , SplinePoint end_point , vec3 end_tangent , vec3 end_up )

Creates a new [spline segment](../../../api/library/worlds/class.splinesegment_usc.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **start_point** - Start [point](../../../api/library/worlds/class.splinepoint_usc.md) of the spline segment.
- *vec3* **start_tangent** - Tangent coordinates for the start point of the spline segment.
- *vec3* **start_up** - Coordinates of the ["up" vector](#up) for the start point of the spline segment.
- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **end_point** - End [point](../../../api/library/worlds/class.splinepoint_usc.md) of the segment.
- *vec3* **end_tangent** - Tangent coordinates for the end point of the spline segment.
- *vec3* **end_up** - Coordinates of the ["up" vector](#up) for the end point of the spline segment.

### Return value

New [spline segment](../../../api/library/worlds/class.splinesegment_usc.md) connecting two specified points.
## void removeSplineSegment ( SplineSegment segment , int with_points = 0 )

Removes the specified spline segment from the world spline graph. You can set the *with_points* flag to remove the segment together with its start and end points.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md)* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_usc.md) to be removed.
- *int* **with_points** - **1** to remove the segment with its start and end points, **0** to keep points. The default value is **0**.

## void getSplineSegments ( )

Returns the list of all segments of the world spline graph and puts them to the specified vector of [SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md) elements.
### Arguments

## void rebuild ( int try_force = 0 )

Rebuilds the world spline graph. This method is to be called after making any changes to spline segments (mode, etc.), point positions, tangents, or "up" vectors, as well as after changing [source node](#source_node) assignments and/or other parameters (UV tiling, gap, etc.)
### Arguments

- *int* **try_force** - Forced rebuild flag: set 1 to try and force rebuild the world spline graph.

## int isRebuilding ( )

Returns a value indicating if the world spline graph is currently being rebuilt. The world spline graph uses a deferred rebuild.
### Return value

1 if the world spline graph is currently being rebuilt; otherwise 0.
## void splitSplineSegment ( SplineSegment segment , float new_point_t )

Splits the specified [spline segment](../../../api/library/worlds/class.splinesegment_usc.md) into two parts by inserting a new point placed at the parametrically specified point on the T (times axis) in the **[0.0f, 1.0f]** range from the segment's start point.
![](../math/cubic_bezier.gif)


### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md)* **segment** - Spline segment to be split.
- *float* **new_point_t** - Coordinate of the splitting point of the segment along the horizontal *T* (times) axis in the range **[0.0f, 1.0f]**.

## void breakSplinePoint ( SplinePoint point )

Breaks the specified [spline point](../../../api/library/worlds/class.splinepoint_usc.md) shared by several [spline segments](../../../api/library/worlds/class.splinesegment_usc.md) into a set of separate ones, so that each of the segments gets its own point.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - Spline point to be broken. > **Notice:** The point must be shared by a least 2 segments.

## int isLinked ( const SplinePoint point )

Returns a value indicating if the specified [spline point](../../../api/library/worlds/class.splinepoint_usc.md) is linked to any [spline segment](../../../api/library/worlds/class.splinesegment_usc.md).
### Arguments

- *const [SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - Spline point to be checked.

### Return value

**1** if the specified spline point is linked to any spline segment; otherwise, **0**.
