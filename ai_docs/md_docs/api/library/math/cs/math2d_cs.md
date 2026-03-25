# Unigine.Math2d Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## Math2d Class

### Members

---

## bool SetPolygonToCCW ( List<vec2> points )

Sets the counter-clockwise orientation for the polygon.
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.

### Return value

true if the counter-clockwise orientation for the polygon is set successfully; otherwise, false.
## void TriangulatePolygon ( List<vec2> points , List<ushort> indices , bool append_to_result )

Performs triangulation by ear clipping algorithm (complexity: O(n^2)/O(n)).
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.
- *List<ushort>* **indices** - List containing all points indices.
- *bool* **append_to_result** - Flag indicating if resulting points should be appended to the points of initial polygon - false (the default value), or replace them - true.

## void ResizePolygon ( List<vec2> points , float offset , List<vec2> result_points , bool append_to_result )

Returns a set of points representing a shrunk/enlarged polygon. Supports concave polygons, CCW and CW orientations.
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.
- *float* **offset**
- *List<vec2>* **result_points** - List containing all points of the shrunk/enlarged polygon.
- *bool* **append_to_result** - Flag indicating if resulting points should be appended to the points of initial polygon - false (the default value), or replace them - true.

## void FindIntersection ( vec2 p1 , vec2 p2 , vec2 p3 , vec2 p4 , bool lines_intersect , bool segments_intersect , vec2 intersection , vec2 close_p1 , vec2 close_p2 )

Finds the point of intersection between the two lines specified by the pairs of points **p1 - p2** and **p3 - p4** and sets the values of the last 5 arguments.
### Arguments

- *vec2* **p1** - Start point coordinates of the first line segment.
- *vec2* **p2** - End point coordinates of the first line segment.
- *vec2* **p3** - Start point coordinates of the second line segment.
- *vec2* **p4** - End point coordinates of the second line segment.
- *bool* **lines_intersect** - true if the lines to which the segments belong intersect; otherwise, false.
- *bool* **segments_intersect** - true if the lines to which the segments belong intersect; otherwise, false.
- *vec2* **intersection** - Coordinates of the point of intersection between the two line segments.
- *vec2* **close_p1** - Coordinates of the first of the two closest points belonging to the first segment.
- *vec2* **close_p2** - Coordinates of the second of the two closest points belonging to the second segment.

## bool PolygonIsOrientedClockwise ( List<vec2> points )

Returns a value indicating if a given polygon is oriented clockwise.
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.

### Return value

true if a given polygon is oriented clockwise; otherwise, false.
## float GetPolygonAreaSigned ( List<vec2> points )

Returns the area of the given polygon in square units.
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.

### Return value


Polygon's area, in square units.


> **Notice:** The value will be negative if the polygon is oriented clockwise.


## float GetPolygonArea ( List<vec2> points )

Returns the area of the given polygon in square units.
### Arguments

- *List<vec2>* **points** - List containing all points of the polygon.

### Return value

Polygon's area, in square units.
## float GetTriangleArea ( vec2 p1 , vec2 p2 , vec2 p3 )

Returns the area of the given triangle in square units.
### Arguments

- *vec2* **p1** - Coordinates of the first triangle vertex.
- *vec2* **p2** - Coordinates of the second triangle vertex.
- *vec2* **p3** - Coordinates of the third triangle vertex.

### Return value


Triangle area, in square units.


> **Notice:** The value will be negative if the polygon is oriented clockwise.


## float Sign ( vec2 point , vec2 segment_p1 , vec2 segment_p2 )

Returns an integral value indicating the sign of an argument.
### Arguments

- *vec2* **point** - Coordinates of the point to be checked.
- *vec2* **segment_p1** - Segment start point coordinates.
- *vec2* **segment_p2** - Segment end point coordinates.

### Return value

Resulting *float* value.
## bool PointTriangleInside ( vec2 point , vec2 v0 , vec2 v1 , vec2 v2 )

Checks if a point is inside a triangle.
### Arguments

- *vec2* **point** - Coordinates of the point to be checked.
- *vec2* **v0** - Coordinates of the first triangle vertex.
- *vec2* **v1** - Coordinates of the second triangle vertex.
- *vec2* **v2** - Coordinates of the third triangle vertex.

### Return value

true if a given point is inside the specified triangle; otherwise, false.
