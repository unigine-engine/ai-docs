# Unigine.SplineSegment Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage individual segments of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_usc.md).


## SplineSegment Class

### Members

---

## void setStartPoint ( SplinePoint point )

Sets the specified spline point as a start point of the segment.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) to be set as a start point of the segment.

## SplinePoint getStartPoint ( )

Returns the current start point of the segment.
### Return value

Start point of the segment.
## void setEndPoint ( SplinePoint point )

Sets the specified spline point as an end point of the segment.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_usc.md)* **point** - [Spline point](../../../api/library/worlds/class.splinepoint_usc.md) to be set as an end point of the segment.

## SplinePoint getEndPoint ( )

Returns the current end point of the segment.
### Return value

End point of the segment.
## void setStartTangent ( vec3 tangent )

Sets the tangent coordinates for the start point of the spline segment.
### Arguments

- *vec3* **tangent** - Start point tangent coordinates to be set.

## vec3 getStartTangent ( )

Returns the current tangent coordinates for the start point of the spline segment.
### Return value

Start point tangent coordinates.
## void setStartUp ( vec3 up )

Sets the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the start point of the segment.
### Arguments

- *vec3* **up** - Start point "up" vector coordinates to be set.

## vec3 getStartUp ( )

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the start point of the spline segment.
### Return value

Start point "up" vector coordinates.
## void setEndTangent ( vec3 tangent )

Sets the tangent coordinates for the end point of the spline segment.
### Arguments

- *vec3* **tangent** - End point tangent coordinates to be set.

## vec3 getEndTangent ( )

Returns the current tangent coordinates for the end point of the spline segment.
### Return value

End point tangent coordinates.
## void setEndUp ( vec3 up )

Sets the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the end point of the segment.
### Arguments

- *vec3* **up** - End point "up" vector coordinates.

## vec3 getEndUp ( )

Returns the current ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the end point of the spline segment.
### Return value

End point "up" vector coordinates to be set.
## void setEnabled ( int enable , int with_points = 1 )

Sets a value indicating whether the spline segment is enabled.
### Arguments

- *int* **enable** - **1** to enable the spline segment, 0 to disable.
- *int* **with_points** - Use **1** to enable all [points](../../../api/library/worlds/class.splinepoint_usc.md) that belong to it as well, 0 to enable the spline point only.

## int isEnabled ( )

Returns a value indicating whether the spline segment is enabled.
### Return value

**1** if the spline segment is enabled; otherwise, **0**.
## Vec3 calcPoint ( float t )

Returns the coordinates of the point at the parametrically specified position on the segment (along the T axis).
![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the **[0.0f, 1.0f]** range.

### Return value

Coordinates of the point.
## vec3 calcTangent ( float t )

Returns the tangent coordinates for the point at the parametrically specified position on the segment (along the T axis).
![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the **[0.0f, 1.0f]** range.

### Return value

Tangent coordinates for the point at the specified position on the segment.
## vec3 calcUpVector ( float t )

Returns the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_usc.md#up) coordinates for the point at the parametrically specified position on the segment (along the T axis).
![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the **[0.0f, 1.0f]** range.

### Return value

Coordinates of the "up" vector for the point at the specified position on the segment.
## float linearToParametric ( float l )

Performs conversion of linear position in accordance with the spline segment's length to parametric position (along the T axis).
![](../math/cubic_bezier.gif)


### Arguments

- *float* **l** - Linear position on the spline segment in the range [0.0f, 1.0f].

### Return value

Parametric position of the point on the segment, along the T (times axis) in the **[0.0f, 1.0f]** range.
## float getLength ( )

Returns the length of the spline segment.
### Return value

Length of the spline segment, in units.
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
## WorldSplineGraph getParent ( )

Returns the *WorldSplineGraph* node to which the spline segment belongs.
### Return value

[*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_usc.md) node to which the spline segment belongs.
## int getNumSources ( )

Returns the total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_usc.md#source_node) assigned to this spline segment.
### Return value

Total number of source nodes assigned to this spline segment.
## int getNumNodes ( )

Returns the total number of nodes placed along the spline segment.
### Return value

Total number of nodes placed along the spline segment.
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
