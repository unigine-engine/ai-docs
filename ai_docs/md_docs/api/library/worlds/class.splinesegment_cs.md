# Unigine.SplineSegment Class (CS)


This class is used to manage individual segments of the [world spline graph](../../../api/library/worlds/class.worldsplinegraph_cs.md) (*WorldSplineGraph*).


## SplineSegment Class

### Properties

## 🔒︎ int NumSources

The total number of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) assigned to this spline segment.
## 🔒︎ int NumNodes

The total number of nodes placed along the spline segment.
## 🔒︎ float Length

The length of the spline segment.
## 🔒︎ WorldSplineGraph Parent

The [*WorldSplineGraph*](../../../api/library/worlds/class.worldsplinegraph_cs.md) node to which the spline segment belongs.
## vec3 EndUp

The ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cs.md#up) coordinates for the end point of the spline segment.
## vec3 EndTangent

The tangent coordinates for the end point of the spline segment.
## vec3 StartUp

The ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cs.md#up) coordinates for the start point of the spline segment.
## vec3 StartTangent

The tangent coordinates for the start point of the spline segment.
## SplinePoint EndPoint

The [Spline point](../../../api/library/worlds/class.splinepoint_cs.md) used as an end point of the segment.
## SplinePoint StartPoint

The [Spline point](../../../api/library/worlds/class.splinepoint_cs.md) used as a start point of the segment.
### Members

---

## void SetEnabled ( bool enable , bool with_points = 1 )

Sets a value indicating whether the spline segment is enabled.
### Arguments

- *bool* **enable** - true to enable the spline segment, false to disable.
- *bool* **with_points** - Use true to enable all [points](../../../api/library/worlds/class.splinepoint_cs.md) that belong to it as well, false to enable the spline point only.

## bool IsEnabled ( )

Returns a value indicating whether the spline segment is enabled.
### Return value

true if the spline segment is enabled; otherwise, false.
## vec3 CalcPoint ( float t )


Returns the coordinates of the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the point.
## vec3 CalcTangent ( float t )


Returns the tangent coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Tangent coordinates for the point at the specified position on the segment.
## vec3 CalcUpVector ( float t )


Returns the ["up" vector](../../../api/library/worlds/class.worldsplinegraph_cs.md#up) coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the "up" vector for the point at the specified position on the segment.
## float LinearToParametric ( float l )


Performs conversion of linear position in accordance with the spline segment's length to parametric position (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *float* **l** - Linear position on the spline segment in the range [0.0f, 1.0f].

### Return value

Parametric position of the point on the segment, along the T (times axis) in the [0.0f, 1.0f] range.
## void ClearSources ( )

Clears the list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) for the spline segment.
## void AssignSource ( string name , int forward_axis = 0 )

Assigns a [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name to the spline segment and sets the specified forward axis for it.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *int* **forward_axis** - Forward axis to be set for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **X** axis is used by default.

## void RemoveSource ( string name , int forward_axis = FORWARD_Y )

Removes the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name.
### Arguments

- *string* **name** - Name of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) to be removed.
- *int* **forward_axis** - Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables. The **Y** axis is used by default.

## void GetSources ( string[] OUT_sources )

Returns a list of [source nodes](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) assigned to the spline segment and puts it to the specified vector.
### Arguments

- *string[]* **OUT_sources** - List of source nodes assigned to the spline segment. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetSegmentMode ( string name , int segment_mode = SEGMENT_TILING )

Sets the segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *int* **segment_mode** - Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_TILING](#SEGMENT_TILING) is used by default.

## int GetSegmentMode ( string name )

Returns the current segment mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Mode for the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name. One of the [SEGMENT_*](#SEGMENT_STRETCH) variables. [SEGMENT_STRETCH](#SEGMENT_STRETCH) is used by default.
## void SetUVTiling ( string name , int enable_uv_tiling = 0 )

Sets a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name is enabled.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *int* **enable_uv_tiling** - **1** to enable UV tiling for the material textures of the source node, **0** - to stretch textures. The default value is **0**.

## int GetUVTiling ( string name )

Returns a value indicating whether UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name is enabled.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

**1** if UV tiling for the material textures of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) is enabled; otherwise (textures are stretched), **0**.
## void SetAdaptiveAngleThreshold ( string name , float adaptive_angle_threshold = 1.0f )


Sets the angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *float* **adaptive_angle_threshold** - Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.

## float GetAdaptiveAngleThreshold ( string name )


Returns the current angle threshold value for splitting [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name. If an angle between the tangents for the two subsequent parts of the spline segment exceeds this value, the node will be split.


> **Notice:** This parameter is used only for the [SEGMENT_ADAPTIVE](#SEGMENT_ADAPTIVE) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Angle threshold value for the source node with the given name, in degrees. The default value is **1.0f**.
## void SetGap ( string name , float gap = 0.0f )


Sets the size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.
- *float* **gap** - Gap size to be set, in units.

## float GetGap ( string name )


Returns the current size of the gap between the adjacent copies of the [source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) with the given name tiled along the spline segment.


> **Notice:** This parameter is used only for the [SEGMENT_TILING](#SEGMENT_TILING) mode.


### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Current gap size, in units.
## void Copy ( SplineSegment src , int copy_endpoints_data = 1 )

Copies all parameters from the specified source spline segment.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)* **src** - Source spline segment.
- *int* **copy_endpoints_data** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_cs.md) as well, 0 to use default ones. The default value is 0.

## SplineSegment Clone ( int clone_points = 0 )

Returns a clone of the spline segment.
### Arguments

- *int* **clone_points** - Use **1** to copy all parameters of segment's [endpoints](../../../api/library/worlds/class.splinepoint_cs.md) as well, 0 to use default ones. The default value is 0.

### Return value

Clone of the spline segment.
## int GetForwardAxis ( string name )

Returns the forward axis used for the source node with the specified name.
### Arguments

- *string* **name** - [Source node](../../../api/library/worlds/class.worldsplinegraph_cs.md#source_node) name.

### Return value

Forward axis for the source node. One of the [FORWARD_](#FORWARD_X) variables.
## Node GetNode ( int index )

Returns a node assigned to the segment by its number.
### Arguments

- *int* **index** - Number of the desired node in a row of nodes placed along the segment in the range from 0 to the [total number of nodes placed along the segment](#getNumNodes_int).

### Return value

Node placed along the segment at the specified position (number).
