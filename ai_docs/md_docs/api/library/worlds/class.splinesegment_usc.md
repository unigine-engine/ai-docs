# Unigine.SplineSegment Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage individual segments of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_usc.md) (*WorldSplineGraph*).


## SplineSegment Class

### Members

## int getNumSources () const

Returns the current total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) assigned to this spline segment.
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
## WorldSplineGraph getParent () const

Returns the current [*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_usc.md) node to which the spline segment belongs.
### Return value

Current *WorldSplineGraph* node to which the spline segment belongs.
## void setEndUp ( vec3 up )

Sets a new ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the end point of the spline segment.
### Arguments

- *vec3* **up** - The End point "up" vector coordinates.

## vec3 getEndUp () const

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the end point of the spline segment.
### Return value

Current End point "up" vector coordinates.
## void setEndTangent ( vec3 tangent )

Sets a new tangent coordinates for the end point of the spline segment.
### Arguments

- *vec3* **tangent** - The End point tangent coordinates to be set.

## vec3 getEndTangent () const

Returns the current tangent coordinates for the end point of the spline segment.
### Return value

Current End point tangent coordinates to be set.
## void setStartUp ( vec3 up )

Sets a new ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the start point of the spline segment.
### Arguments

- *vec3* **up** - The Start point "up" vector coordinates.

## vec3 getStartUp () const

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the start point of the spline segment.
### Return value

Current Start point "up" vector coordinates.
## void setStartTangent ( vec3 tangent )

Sets a new tangent coordinates for the start point of the spline segment.
### Arguments

- *vec3* **tangent** - The Start point tangent coordinates.

## vec3 getStartTangent () const

Returns the current tangent coordinates for the start point of the spline segment.
### Return value

Current Start point tangent coordinates.
## void setEndPoint ( SplinePoint point )

Sets a new [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) used as an end point of the segment.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - The End point of the segment.

## SplinePoint getEndPoint () const

Returns the current [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) used as an end point of the segment.
### Return value

Current End point of the segment.
## void setStartPoint ( SplinePoint point )

Sets a new [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) used as a start point of the segment.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - The start point of the segment.

## SplinePoint getStartPoint () const

Returns the current [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) used as a start point of the segment.
### Return value

Current start point of the segment.
---

## void setEnabled ( int enable , int with_points = 1 )

Sets a value indicating whether the spline segment is enabled.
### Arguments

- *int* **enable** - **1** to enable the spline segment, **0** to disable.
- *int* **with_points** - Use **1** to enable all [points](../../../api/library/worlds/class.splinepoint_usc.md) that belong to it as well, **0** to enable the spline point only.

## int isEnabled ( )

Returns a value indicating whether the spline segment is enabled.
### Return value

**1** if the spline segment is enabled; otherwise, **0**.
## Vec3 calcPoint ( float t )


Returns the coordinates of the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the point.
## vec3 calcTangent ( float t )


Returns the tangent coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Tangent coordinates for the point at the specified position on the segment.
## vec3 calcUpVector ( float t )


Returns the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the "up" vector for the point at the specified position on the segment.
## float linearToParametric ( float l )


Performs conversion of linear position in accordance with the spline segment's length to parametric position (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **l** - Linear position on the spline segment in the range [0.0f, 1.0f].

### Return value

Parametric position of the point on the segment, along the T (times axis) in the [0.0f, 1.0f] range.
## void clearSources ( )

Clears the list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) for the spline segment.
## void assignSource ( string name , int forward_axis = 0 )

Assigns a [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name to the spline segment and sets the specified forward axis for it.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.
- *int* **forward_axis** - Forward axis to be set for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **X** axis is used by default.

## void removeSource ( string name , int forward_axis = FORWARD_Y )

Removes the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name.
### Arguments

- *string* **name** - Name of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) to be removed.
- *int* **forward_axis** - Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **Y** axis is used by default.

## void getSources ( )

Returns a list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) assigned to the spline segment and puts it to the specified vector.
### Arguments

## void setSegmentMode ( string name , int segment_mode = SEGMENT_TILING )

Sets the segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.
- *int* **segment_mode** - Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_TILING](#SEGMENT_TILING) is used by default.

## int getSegmentMode ( string name )

Returns the current segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.

### Return value

Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_STRETCH](#SEGMENT_STRETCH) is used by default.
## void setUVTiling ( string name , int enable_uv_tiling = 0 )

Sets a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name is enabled.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.
- *int* **enable_uv_tiling** - **1** to enable UV tiling for the material textures of the source node, **0** - to stretch textures. The default value is **0**.

## int getUVTiling ( string name )

Returns a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name is enabled.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.

### Return value

**1** if UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) is enabled; otherwise (textures are stretched), **0**.
## void setAdaptiveAngleThreshold ( string name , float adaptive_angle_threshold = 1.0f )


Sets the angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.
- *float* **adaptive_angle_threshold** - Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.

## float getAdaptiveAngleThreshold ( string name )


Returns the current angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.

### Return value

Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.
## void setGap ( string name , float gap = 0.0f )


Sets the size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.
- *float* **gap** - Gap size to be set, in units.

## float getGap ( string name )


Returns the current size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.

### Return value

Current gap size, in units.
## void copy ( const SplineSegment src , int copy_endpoints_data = 1 )

Copies all parameters from the specified source spline segment.
### Arguments

- *const [SplineSegment](../../../api/library/worlds/class.splinesegment_usc.md)* **src** - Source spline segment.
- *int* **copy_endpoints_data** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_usc.md) as well, 0 to use default ones. The default value is 0.

## SplineSegment clone ( int clone_points = 0 )

Returns a clone of the spline segment.
### Arguments

- *int* **clone_points** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_usc.md) as well, 0 to use default ones. The default value is 0.

### Return value

Clone of the spline segment.
## int getForwardAxis ( string name )

Returns the forward axis used for the source node with the specified name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) name.

### Return value

Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables.
## Node getNode ( int index )

Returns a node assigned to the segment by its number.
### Arguments

- *int* **index** - Number of the desired node in a row of nodes placed along the segment in the range from 0 to the [total number of nodes placed along the segment](#getNumNodes_int).

### Return value

Node placed along the segment at the specified position (number).
