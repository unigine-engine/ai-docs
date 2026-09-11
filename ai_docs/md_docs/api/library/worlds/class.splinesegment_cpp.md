# Unigine.SplineSegment Class (CPP)

**Header:** #include <UnigineWorlds.h>


This class is used to manage individual segments of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_cpp.md) (*WorldSplineGraph*).


## SplineSegment Class

### Members

## int getNumSources () const

Returns the current total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) assigned to this spline segment.
### Return value

Current total number of source nodes assigned to this spline segment.
## int getNumNodes () const

Returns the current total number of nodes placed along the spline segment.
### Return value

Current total number of nodes placed along the spline segment.
## float getLength () const

Returns the current length of the spline segment.
### Return value

Current length of the spline segment, in units.
## Ptr < WorldSplineGraph > getParent () const

Returns the current [*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_cpp.md) node to which the spline segment belongs.
### Return value

Current *WorldSplineGraph* node to which the spline segment belongs.
## void setEndUp ( const Math::vec3&& up )

Sets a new ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cpp.md#up) coordinates for the end point of the spline segment.
### Arguments

- *const  Math::vec3&&* **up** - The End point "up" vector coordinates.

## Math::vec3& getEndUp () const

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cpp.md#up) coordinates for the end point of the spline segment.
### Return value

Current End point "up" vector coordinates.
## void setEndTangent ( const Math::vec3&& tangent )

Sets a new tangent coordinates for the end point of the spline segment.
### Arguments

- *const  Math::vec3&&* **tangent** - The End point tangent coordinates to be set.

## Math::vec3& getEndTangent () const

Returns the current tangent coordinates for the end point of the spline segment.
### Return value

Current End point tangent coordinates to be set.
## void setStartUp ( const Math::vec3&& up )

Sets a new ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cpp.md#up) coordinates for the start point of the spline segment.
### Arguments

- *const  Math::vec3&&* **up** - The Start point "up" vector coordinates.

## Math::vec3& getStartUp () const

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cpp.md#up) coordinates for the start point of the spline segment.
### Return value

Current Start point "up" vector coordinates.
## void setStartTangent ( const Math::vec3&& tangent )

Sets a new tangent coordinates for the start point of the spline segment.
### Arguments

- *const  Math::vec3&&* **tangent** - The Start point tangent coordinates.

## Math::vec3& getStartTangent () const

Returns the current tangent coordinates for the start point of the spline segment.
### Return value

Current Start point tangent coordinates.
## void setEndPoint ( const Ptr < SplinePoint >& point )

Sets a new [Spline point](../../../api/library/worlds/class.splinepoint_cpp.md) used as an end point of the segment.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)>&* **point** - The End point of the segment.

## Ptr < SplinePoint > getEndPoint () const

Returns the current [Spline point](../../../api/library/worlds/class.splinepoint_cpp.md) used as an end point of the segment.
### Return value

Current End point of the segment.
## void setStartPoint ( const Ptr < SplinePoint >& point )

Sets a new [Spline point](../../../api/library/worlds/class.splinepoint_cpp.md) used as a start point of the segment.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)>&* **point** - The start point of the segment.

## Ptr < SplinePoint > getStartPoint () const

Returns the current [Spline point](../../../api/library/worlds/class.splinepoint_cpp.md) used as a start point of the segment.
### Return value

Current start point of the segment.
---

## void setEnabled ( bool enable , bool with_points = 1 )

Sets a value indicating whether the spline segment is enabled.
### Arguments

- *bool* **enable** - true to enable the spline segment, false to disable.
- *bool* **with_points** - Use true to enable all [points](../../../api/library/worlds/class.splinepoint_cpp.md) that belong to it as well, false to enable the spline point only.

## bool isEnabled ( ) const

Returns a value indicating whether the spline segment is enabled.
### Return value

true if the spline segment is enabled; otherwise, false.
## Math:: Vec3 calcPoint ( float t ) const


Returns the coordinates of the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the point.
## Math:: vec3 calcTangent ( float t ) const


Returns the tangent coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Tangent coordinates for the point at the specified position on the segment.
## Math:: vec3 calcUpVector ( float t ) const


Returns the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cpp.md#up) coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the "up" vector for the point at the specified position on the segment.
## float linearToParametric ( float l ) const


Performs conversion of linear position in accordance with the spline segment's length to parametric position (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **l** - Linear position on the spline segment in the range [0.0f, 1.0f].

### Return value

Parametric position of the point on the segment, along the T (times axis) in the [0.0f, 1.0f] range.
## void clearSources ( )

Clears the list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) for the spline segment.
## void assignSource ( const char * name , int forward_axis = 0 )

Assigns a [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name to the spline segment and sets the specified forward axis for it.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *int* **forward_axis** - Forward axis to be set for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **X** axis is used by default.

## void removeSource ( const char * name , int forward_axis = FORWARD_Y )

Removes the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name.
### Arguments

- *const char ** **name** - Name of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) to be removed.
- *int* **forward_axis** - Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **Y** axis is used by default.

## void getSources ( Vector < String > & OUT_sources ) const

Returns a list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) assigned to the spline segment and puts it to the specified vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **OUT_sources** - List of source nodes assigned to the spline segment. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setSegmentMode ( const char * name , int segment_mode = SEGMENT_TILING )

Sets the segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *int* **segment_mode** - Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_TILING](#SEGMENT_TILING) is used by default.

## int getSegmentMode ( const char * name ) const

Returns the current segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_STRETCH](#SEGMENT_STRETCH) is used by default.
## void setUVTiling ( const char * name , int enable_uv_tiling = 0 )

Sets a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name is enabled.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *int* **enable_uv_tiling** - **1** to enable UV tiling for the material textures of the source node, **0** - to stretch textures. The default value is **0**.

## int getUVTiling ( const char * name ) const

Returns a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name is enabled.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

**1** if UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) is enabled; otherwise (textures are stretched), **0**.
## void setAdaptiveAngleThreshold ( const char * name , float adaptive_angle_threshold = 1.0f )


Sets the angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *float* **adaptive_angle_threshold** - Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.

## float getAdaptiveAngleThreshold ( const char * name ) const


Returns the current angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.
## void setGap ( const char * name , float gap = 0.0f )


Sets the size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.
- *float* **gap** - Gap size to be set, in units.

## float getGap ( const char * name ) const


Returns the current size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Current gap size, in units.
## void copy ( const Ptr < SplineSegment > & src , int copy_endpoints_data = 1 )

Copies all parameters from the specified source spline segment.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> &* **src** - Source spline segment.
- *int* **copy_endpoints_data** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_cpp.md) as well, 0 to use default ones. The default value is 0.

## Ptr < SplineSegment > clone ( int clone_points = 0 )

Returns a clone of the spline segment.
### Arguments

- *int* **clone_points** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_cpp.md) as well, 0 to use default ones. The default value is 0.

### Return value

Clone of the spline segment.
## int getForwardAxis ( const char * name )

Returns the forward axis used for the source node with the specified name.
### Arguments

- *const char ** **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cpp.md#source_node) name.

### Return value

Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables.
## Ptr < Node > getNode ( int index )

Returns a node assigned to the segment by its number.
### Arguments

- *int* **index** - Number of the desired node in a row of nodes placed along the segment in the range from 0 to the [total number of nodes placed along the segment](#getNumNodes_int).

### Return value

Node placed along the segment at the specified position (number).
