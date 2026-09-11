# Math 2D Functions (CPP)

**Header:** #include <UnigineMathLib2d.h>


This class represents a collection of two-dimensional math functions.


> **Notice:** Math 2D functions are the members of the **Unigine::Math** namespace.


## Math Class

### Members

---

## void findIntersection ( const vec2 & p1 , const vec2 & p2 , const vec2 & p3 , const vec2 & p4 , int & lines_intersect , int & segments_intersect , vec2 & intersection , vec2 & close_p1 , vec2 & close_p2 )

Finds the point of intersection between the two lines specified by the pairs of points **p1 - p2** and **p3 - p4** and fills in the values of the last 5 arguments.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p1** - Start point coordinates of the first line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p2** - End point coordinates of the first line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p3** - Start point coordinates of the second line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p4** - End point coordinates of the second line segment.
- *int &* **lines_intersect** - 1 if the lines to which the segments belong intersect; otherwise, 0.
- *int &* **segments_intersect** - 1 if the segments intersect; otherwise, 0.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **intersection** - Coordinates of the point of intersection between the two line segments.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **close_p1** - Coordinates of the first of the two closest points belonging to the first segment.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **close_p2** - Coordinates of the second of the two closest points belonging to the second segment.

## int findIntersection ( const vec2 & p1 , const vec2 & p2 , const vec2 & p3 , const vec2 & p4 , vec2 & intersection )

Finds the point of intersection between the two lines specified by the pairs of points **p1 - p2** and **p3 - p4**.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p1** - Start point coordinates of the first line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p2** - End point coordinates of the first line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p3** - Start point coordinates of the second line segment.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p4** - End point coordinates of the second line segment.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **intersection** - Coordinates of the point of intersection between the two line segments.

### Return value

1 if the segments intersect; otherwise, 0.
## void findIntersection ( const dvec2 & p1 , const dvec2 & p2 , const dvec2 & p3 , const dvec2 & p4 , int & lines_intersect , int & segments_intersect , vec2 & intersection , vec2 & close_p1 , vec2 & close_p2 )

Finds the point of intersection between the two lines specified by the pairs of points **p1 - p2** and **p3 - p4** and fills in the values of the last 5 arguments.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p1** - Start point coordinates of the first line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p2** - End point coordinates of the first line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p3** - Start point coordinates of the second line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p4** - End point coordinates of the second line segment.
- *int &* **lines_intersect** - 1 if the lines to which the segments belong intersect; otherwise, 0.
- *int &* **segments_intersect** - 1 if the segments intersect; otherwise, 0.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **intersection** - Coordinates of the point of intersection between the two line segments.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **close_p1** - Coordinates of the first of the two closest points belonging to the first segment.
- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **close_p2** - Coordinates of the second of the two closest points belonging to the second segment.

## int findIntersection ( const dvec2 & p1 , const dvec2 & p2 , const dvec2 & p3 , const dvec2 & p4 , dvec2 & intersection )

Finds the point of intersection between the two lines specified by the pairs of points **p1 - p2** and **p3 - p4**.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p1** - Start point coordinates of the first line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p2** - End point coordinates of the first line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p3** - Start point coordinates of the second line segment.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **p4** - End point coordinates of the second line segment.
- *[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **intersection** - Coordinates of the point of intersection between the two line segments.

### Return value

1 if the segments intersect; otherwise, 0.
## float getPolygonArea ( const Vector < vec2 > & points )

Returns the area of the given polygon in square units.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.

### Return value

Polygon's area, in square units.
## float getPolygonAreaSigned ( const Vector < vec2 > & points )

Returns the area of the given polygon in square units.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.

### Return value


Polygon's area, in square units.


> **Notice:** The negative value means that the polygon is oriented clockwise.


## float getTriangleArea ( const vec2 & p1 , const vec2 & p2 , const vec2 & p3 )

Returns the area of the given triangle in square units.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p1** - Coordinates of the first triangle vertex.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p2** - Coordinates of the second triangle vertex.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **p3** - Coordinates of the third triangle vertex.

### Return value


Triangle area, in square units.


> **Notice:** The negative value means that the polygon is oriented clockwise.


## int pointTriangleInside ( const vec2 & point , const vec2 & v0 , const vec2 & v1 , const vec2 & v2 )

Returns a value indicating if a given point is inside the specified triangle.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of the point to be checked.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Coordinates of the first triangle vertex.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Coordinates of the second triangle vertex.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - Coordinates of the third triangle vertex.

### Return value

1 if a given point is inside the specified triangle; otherwise, 0.
## int polygonIsOrientedClockwise ( const Vector < vec2 > & points )

Returns a value indicating if a given polygon is oriented clockwise.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.

### Return value

1 if a given polygon is oriented clockwise; otherwise, 0.
## void resizePolygon ( const Vector < vec2 > & points , float offset , Vector < vec2 > & result_points , int append_to_result )

Returns a set of points representing a resized polygon. The polygon is modified by moving its edges inward or outward by a specified offset. This is commonly referred to as "inflating" or "deflating" a polygon, depending on whether the offset is positive (expansion) or negative (contraction). Supports concave polygons, CCW and CW orientations.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.
- *float* **offset** - The value to which each polygon point is moved outward (positive value) or inward (negative value).
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **result_points** - Vector containing all points of the deflated/inflated polygon.
- *int* **append_to_result** - Flag indicating if resulting points should be appended to the points of initial polygon - 0 (the default value), or replace them - 1.

## int setPolygonToCCW ( Vector < vec2 > & points )

Sets the counter-clockwise orientation for the polygon.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.

### Return value

1 if the counter-clockwise orientation for the polygon is set successfully; otherwise, 0.
## float sign ( const vec2 & point , const vec2 & segment_p1 , const vec2 & segment_p2 )

Returns a value indicating to which part of the segment the point belongs.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of the point to be checked.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **segment_p1** - Segment start point coordinates.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **segment_p2** - Segment end point coordinates.

## void triangulatePolygon ( const Vector < vec2 > & points , Vector <unsigned short> & indices , int append_to_result )

Performs triangulation by ear clipping algorithm (complexity: O(n^2)/O(n)).
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Vector containing all points of the polygon.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<unsigned short> &* **indices** - Vector containing all points indices.
- *int* **append_to_result** - Flag indicating if resulting points should be appended to the points of initial polygon - 0 (the default value), or replace them - 1.
