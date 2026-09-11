# Unigine.SplinePoint Class (CPP)

**Header:** #include <UnigineWorlds.h>


This class is used to manage individual points of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_cpp.md) (*WorldSplineGraph*).


## SplinePoint Class

### Members

## int getNumSources () const

Returns the current total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) assigned to this spline point.
### Return value

Current total number of source nodes assigned to this spline point.
## int getNumSegments () const

Returns the current total number of [segments](../../../api/library/worlds/class.splinesegment_cpp.md) sharing this spline point.
### Return value

Current total number of segments sharing this spline point.
## void setPosition ( const Math:: Vec3 & position )

Sets a new position of the spline point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The position of the spline point.

## Math:: Vec3 getPosition () const

Returns the current position of the spline point.
### Return value

Current position of the spline point.
## Ptr < WorldSplineGraph > getParent () const

Returns the current [*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_cpp.md) node to which the spline point belongs.
### Return value

Current *WorldSplineGraph* node to which the spline point belongs.
## int getNumNodes () const

Returns the current total number of nodes placed at this spline point.
### Return value

Current total number of nodes placed at this spline point.
---

## void setEnabled ( bool enable , bool with_segments = 1 )

Sets a value indicating whether the spline point is enabled.
### Arguments

- *bool* **enable** - **1** to enable the spline point, 0 to disable.
- *bool* **with_segments** - Use true to enable all [segments](../../../api/library/worlds/class.splinesegment_cpp.md), to which the point belongs as well, false to enable the spline point only.

## bool isEnabled ( ) const

Returns a value indicating whether the spline point is enabled.
### Return value

true if the spline point is enabled; otherwise, false.
## void getSplineSegments ( Vector < Ptr < SplineSegment > > & OUT_segments ) const

Returns the list of segments, to which the spline point belongs, and puts them to the specified vector of [SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md) elements.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> > &* **OUT_segments** - Vector to store the list of segments, to which the spline point belongs. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void clearSources ( )

Clears the list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) for the spline point.
## void assignSource ( const char * name )

Assigns a [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name to the spline point.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

## void removeSource ( const char * name )

Removes the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name.
### Arguments

- *const char ** **name** - Name of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) to be removed.

## void getSources ( Vector < String > & OUT_sources ) const

Returns a list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) assigned to the spline point and puts it to the specified vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **OUT_sources** - List of source nodes assigned to the spline point. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void copy ( const Ptr < SplinePoint > & src )

Copies all parameters from the specified source spline point.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **src** - Source spline point.

## Ptr < SplinePoint > clone ( )

Returns a clone of the spline point.
### Return value

Clone of the spline point.
## int getSourceNodeType ( const char * name ) const

Returns the type of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the specified name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Source node type.
## void setLinkVariant ( const char * name , int variant )

Sets a link variant for the junction source node with the specified name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *int* **variant** - Link variant number for the junction source node.

## int getLinkVariant ( const char * name ) const

Returns the current link variant for the junction source node with the specified name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Link variant number for the junction source node.
## int getLinkWorldPosition ( const Ptr < SplineSegment > & segment , Math:: Vec3 & position ) const

Gets the current link (bone) position of the junction source node and puts it to the specified *position* vector.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> &* **segment** - Spline segment for which the position of the corresponding link (bone) of the junction source node is to be obtained.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Vector to store the position of the junction source node's link (bone) corresponding to the specified [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md).

### Return value

1 if the current position of the junction source node's link (bone) corresponding to the specified spline segment was obtained successfully; otherwise 0.
## Ptr < Node > getNode ( int index )

Returns a node assigned to the point by its number.
### Arguments

- *int* **index** - Number of the desired node in a row of nodes placed at this point, in the range from 0 to the [total number of nodes placed at the point](#getNumNodes_int).

### Return value

Node placed at this point at the specified position (number).
