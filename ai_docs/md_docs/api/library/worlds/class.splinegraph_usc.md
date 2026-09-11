# Unigine.SplineGraph Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage vertices and segments of spline graphs. UNIGINE's 3D spline system has a wide range of applications, particularly procedural content generation (rivers, roads, pipelines etc.).


![](../../../code/formats/spline.png)


A spline graph is determined by a set of points **p0, p1, ... pn** and a set of segments (cubic Bezier splines), that connect some or all of these points.


Each **segment** is determined by the indices of the starting (**pSTART**) and ending (**pEND**) points and tangent vector coordinates at these points, which determine the form of the segment (**tSTART** and **tEND** respectively).


Coordinates of the **"up" vector** are additionally stored for each point of the segment. You can specify this vector to define orientation of geometry or objects, that can be [stretched or tiled along the segments](../../../api/library/worlds/class.worldsplinegraph_usc.md#intro) of the spline graph. By default this vector is parallel to the **Z** axis. The "up" vector does not affect the form of the spline segment.


It is possible to obtain an interpolated value for any point belonging to a segment, this can be used for various purposes (e.g. to change road profile). Interpolated "up" vector can be calculated as follows (pseudocode):


```cpp
vec3 lerpUpVector(vec3 start_up, vec3 end_up, float t) const
{
	float angle = acos(dot(start_up, end_up)) * RAD2DEG;
	vec3 rotation_axis = cross(start_up, end_up);

	return rotateAxisAngle(rotation_axis, angle * t) * start_up;
}

```


### See Also


- C++ sample
- UnigineScript sample
- The [WorldSplineGraph](../../../api/library/worlds/class.worldsplinegraph_usc.md) class article to learn how to generate geometry along a spline graph
- The [Spline File Format](../../../code/formats/spline_format.md) article to learn how the spline graph data is stored


## SplineGraph Class

### Members

## int getNumSegments () const

Returns the current total number of segments in the spline graph.
### Return value

Current total number of segments in the spline graph.
## int getNumPoints () const

Returns the current total number of points in the spline graph.
### Return value

Current total number of points in the spline graph.
---

## static SplineGraph ( )

Default constructor. Creates an empty spline graph.
## static SplineGraph ( string name )

Constructor. Creates an empty spline graph with a given name.
### Arguments

- *string* **name** - Spline graph name.

## float getLength ( int index )

Returns the length of the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Segment length.
## void setPoint ( int index , Vec3 point )

Sets new coordinates for the point with a given index.
### Arguments

- *int* **index** - Point index.
- *Vec3* **point** - New point coordinates.

## Vec3 getPoint ( int index )

Returns the coordinates of the point with a given index.
### Arguments

- *int* **index** - Point index.

### Return value

Point coordinates.
## void setSegmentEndPoint ( int index , Vec3 point )

Sets the coordinates of the end point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *Vec3* **point** - Segment end point coordinates to be set.

## Vec3 getSegmentEndPoint ( int index )

Returns the coordinates of the end point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Segment end point coordinates.
## int getSegmentEndPointIndex ( int index )

Returns the index of the end point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Segment end point index.
## void setSegmentEndTangent ( int index , vec3 tangent )

Sets the tangent coordinates for the end point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *vec3* **tangent** - End point tangent coordinates.

## vec3 getSegmentEndTangent ( int index )

Returns the tangent coordinates for the end point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

End point tangent coordinates.
## void setSegmentEndUpVector ( int index , vec3 up )

Sets the "up" vector coordinates for the end point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *vec3* **up** - End point ["up" vector coordinates](#up).

## vec3 getSegmentEndUpVector ( int index )

Returns the "up" vector coordinates for the end point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

End point ["up" vector coordinates](#up).
## void setSegmentStartPoint ( int index , Vec3 point )

Sets the coordinates of the start point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *Vec3* **point** - Segment start point coordinates to be set.

## Vec3 getSegmentStartPoint ( int index )

Returns the coordinates of the start point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Segment start point coordinates.
## int getSegmentStartPointIndex ( int index )

Returns the index of the end point for the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Segment start point index.
## void setSegmentStartTangent ( int index , vec3 tangent )

Sets the tangent coordinates for the start point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *vec3* **tangent** - Start point tangent coordinates.

## vec3 getSegmentStartTangent ( int index )

Returns the tangent coordinates for the start point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Start point tangent coordinates.
## void setSegmentStartUpVector ( int index , vec3 up )

Sets the "up" vector coordinates for the start point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *vec3* **up** - Start point ["up" vector coordinates](#up).

## vec3 getSegmentStartUpVector ( int index )

Returns the "up" vector coordinates for the start point of the segment with a given index.
### Arguments

- *int* **index** - Segment index.

### Return value

Start point ["up" vector coordinates](#up).
## int addPoint ( Vec3 point )

Adds a point with specified coordinates to the spline graph.
### Arguments

- *Vec3* **point** - Point coordinates.

### Return value

Current number of points in the spline graph.
## int addSegment ( int start_index , vec3 start_tangent , vec3 start_up , int end_index , vec3 end_tangent , vec3 end_up )

Adds a segment to the spline graph.
### Arguments

- *int* **start_index** - Start point index.
- *vec3* **start_tangent** - Start point tangent coordinates.
- *vec3* **start_up** - Start point ["up" vector coordinates](#up).
- *int* **end_index** - End point index.
- *vec3* **end_tangent** - End point tangent coordinates.
- *vec3* **end_up** - End point ["up" vector coordinates](#up).

### Return value

Number of segments in the spline graph if a segment was adds successfully; otherwise, -1
## Vec3 calcSegmentPoint ( int index , float t )


Returns the coordinates of the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *int* **index** - Segment index.
- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Coordinates of the point on the given segment.
## vec3 calcSegmentTangent ( int index , float t )


Returns the tangent coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *int* **index** - Segment index.
- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

Tangent coordinates for the point on the given segment.
## vec3 calcSegmentUpVector ( int index , float t )


Returns the "up" vector coordinates for the point at the parametrically specified position on the segment (along the T axis).


![](../math/cubic_bezier.gif)


### Arguments

- *int* **index** - Segment index.
- *float* **t** - Position of the point on the segment, specified parametrically along the T (times axis) in the [0.0f, 1.0f] range.

### Return value

"Up" vector coordinates for the point on the given segment.
## void clear ( )

Clears the spline graph.
## int load ( string name )

Loads the spline graph from the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to load the spline graph from.

### Return value

**1** if the spline graph was successfully loaded; otherwise, **0**.
## void removePoint ( int index , int merge = 0 )

Removes a point with a given index from the spline graph.
### Arguments

- *int* **index** - Point index.
- *int* **merge** - Merge flag. When there are two segments attached to the point, use **1** to merge these segments into one; **0** removes all segments attached to the point (by default).

## void splitPoint ( int index )

Splits the point with the specified index into **N** points, where **N** is the number of segments attached to the point. The number of points in the graph shall increase by **N-1**. All new points will be attached to the corresponding segments.
### Arguments

- *int* **index** - Point index.

## void weldPoints ( Vector<int>& OUT_indices )


Merges all points with given indices into one.


> **Notice:** All common segments between these points shall be removed. All points with given indices are removed from the graph, except for the one having the minimum index value, all segments shall be attached to this point. Resulting point shall be moved to the position of the first point in the given array.


### Arguments

- *Vector<int>&* **OUT_indices** - Array containing indices of points to be merged into one. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void removeSegment ( int index , int with_points = 0 )

Removes the segment with a given index.
### Arguments

- *int* **index** - Segment index.
- *int* **with_points** - Use true to remove segment with its starting and ending points, or false to remove the segment only. > **Notice:** Points will be removed only in case if they do not belong to other segments. After removal, the last element of the vector of spline graph segments shall be moved to the position of the one removed.

## int save ( string name )

Saves the spline graph to the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to save the spline graph to.

### Return value

**1** if the spline graph was successfully saved; otherwise, **0**.
## void insertPointToSegment ( int segment_index , float new_point_t )


Inserts a new point into the given segment. The point is parametrically specified on the T (times axis) in the [0.0f, 1.0f] range from the segment's start point.


![](../math/cubic_bezier.gif)

### Arguments

- *int* **segment_index** - Segment index.
- *float* **new_point_t** - Coordinate of the new point to be added along the horizontal *T* (times) axis in the range [0.0f, 1.0f].

## void getPointSegmentsIndices ( int index , Vector<int>& OUT_indices )

Retrieves indices of all segments attached to the specified point and puts them to the given index buffer.
### Arguments

- *int* **index** - Point index.
- *Vector<int>&* **OUT_indices** - Index buffer to which segment indices will be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
