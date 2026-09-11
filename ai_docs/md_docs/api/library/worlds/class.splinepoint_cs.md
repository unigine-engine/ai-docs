# Unigine.SplinePoint Class (CS)


This class is used to manage individual points of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_cs.md) (*WorldSplineGraph*).


## SplinePoint Class

### Properties

## 🔒︎ int NumSources

The total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) assigned to this spline point.
## 🔒︎ int NumSegments

The total number of [segments](../../../api/library/worlds/class.splinesegment_cs.md) sharing this spline point.
## vec3 Position

The position of the spline point.
## 🔒︎ WorldSplineGraph Parent

The [*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_cs.md) node to which the spline point belongs.
## 🔒︎ int NumNodes

The total number of nodes placed at this spline point.
### Members

---

## void SetEnabled ( bool enable , bool with_segments = 1 )

Sets a value indicating whether the spline point is enabled.
### Arguments

- *bool* **enable** - **1** to enable the spline point, 0 to disable.
- *bool* **with_segments** - Use true to enable all [segments](../../../api/library/worlds/class.splinesegment_cs.md), to which the point belongs as well, false to enable the spline point only.

## bool IsEnabled ( )

Returns a value indicating whether the spline point is enabled.
### Return value

true if the spline point is enabled; otherwise, false.
## void GetSplineSegments ( SplineSegment [] OUT_segments )

Returns the list of segments, to which the spline point belongs, and puts them to the specified array of [SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md) elements.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)[]* **OUT_segments** - Array to store the list of segments, to which the spline point belongs. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void ClearSources ( )

Clears the list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) for the spline point.
## void AssignSource ( string name )

Assigns a [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name to the spline point.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

## void RemoveSource ( string name )

Removes the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name.
### Arguments

- *string* **name** - Name of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) to be removed.

## void GetSources ( string[] OUT_sources )

Returns a list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) assigned to the spline point and puts it to the specified vector.
### Arguments

- *string[]* **OUT_sources** - List of source nodes assigned to the spline point. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Copy ( SplinePoint src )

Copies all parameters from the specified source spline point.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **src** - Source spline point.

## SplinePoint Clone ( )

Returns a clone of the spline point.
### Return value

Clone of the spline point.
## int GetSourceNodeType ( string name )

Returns the type of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the specified name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Source node type.
## void SetLinkVariant ( string name , int variant )

Sets a link variant for the junction source node with the specified name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *int* **variant** - Link variant number for the junction source node.

## int GetLinkVariant ( string name )

Returns the current link variant for the junction source node with the specified name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Link variant number for the junction source node.
## int GetLinkWorldPosition ( SplineSegment segment , out Vec3 position )

Gets the current link (bone) position of the junction source node and puts it to the specified *position* vector.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)* **segment** - Spline segment for which the position of the corresponding link (bone) of the junction source node is to be obtained.
- *out Vec3* **position** - Vector to store the position of the junction source node's link (bone) corresponding to the specified [spline segment](../../../api/library/worlds/class.splinesegment_cs.md).

### Return value

1 if the current position of the junction source node's link (bone) corresponding to the specified spline segment was obtained successfully; otherwise 0.
## Node GetNode ( int index )

Returns a node assigned to the point by its number.
### Arguments

- *int* **index** - Number of the desired node in a row of nodes placed at this point, in the range from 0 to the [total number of nodes placed at the point](#getNumNodes_int).

### Return value

Node placed at this point at the specified position (number).
