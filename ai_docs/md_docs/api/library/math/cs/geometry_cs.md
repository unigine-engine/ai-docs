# Geometry Functions (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This class is used to represent a collection of generic 3d math functions such as line plane intersection, closest points on two lines, etc.


## Geometry Class

### Members

---

## void OrthoBasis ( vec3 v , vec3 tangent , vec3 binormal )

Creates an ortho transformation. Output tangent and binormal vectors will be put to corresponding return vectors.
### Arguments

- *vec3* **v** - Input vector.
- *vec3* **tangent** - Return tangent vector.
- *vec3* **binormal** - Return binormal vector.

## void OrthoBasis ( dvec3 v , dvec3 tangent , dvec3 binormal )

Creates an ortho transformation. Output tangent and binormal vectors will be put to corresponding return vectors.
### Arguments

- *dvec3* **v** - Input vector.
- *dvec3* **tangent** - Return tangent vector.
- *dvec3* **binormal** - Return binormal vector.

## void OrthoTransform ( vec3 v , mat4 transform )

Creates an ortho transformation. The transformation will be put to the transformation matrix.
### Arguments

- *vec3* **v** - Input vector.
- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void OrthoTransform ( dvec3 v , dmat4 transform )

Creates an ortho transformation. The transformation will be put to the transformation matrix.
### Arguments

- *dvec3* **v** - Input vector.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## quat OrthoTangent ( vec4 t , vec3 n )

Creates the ortho triangle tangent space basis.
### Arguments

- *vec4* **t** - Tangent vector.
- *vec3* **n** - Normal vector.

### Return value

Tangent basis.
## quat OrthoTangent ( vec3 t , vec3 b , vec3 n )

Creates the ortho triangle tangent space basis.
### Arguments

- *vec3* **t** - Tangent vector.
- *vec3* **b** - Binormal vector.
- *vec3* **n** - Normal vector.

### Return value

Tangent basis.
## float TriangleArea ( vec3 v0 , vec3 v1 , vec3 v2 )

Returns the triangle area.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.

### Return value

Triangle area.
## double TriangleArea ( dvec3 v0 , dvec3 v1 , dvec3 v2 )

Returns the triangle area.
### Arguments

- *dvec3* **v0** - The first triangle vertex.
- *dvec3* **v1** - The second triangle vertex.
- *dvec3* **v2** - The third triangle vertex.

### Return value

Triangle area.
## vec3 TriangleNormal ( vec3 v0 , vec3 v1 , vec3 v2 )

Returns the triangle normal vector.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.

### Return value

Triangle normal vector.
## dvec3 TriangleNormal ( dvec3 v0 , dvec3 v1 , dvec3 v2 )

Returns the triangle normal vector.
### Arguments

- *dvec3* **v0** - The first triangle vertex.
- *dvec3* **v1** - The second triangle vertex.
- *dvec3* **v2** - The third triangle vertex.

### Return value

Triangle normal vector.
## vec4 TrianglePlane ( vec3 v0 , vec3 v1 , vec3 v2 )

Returns the triangle plane.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.

### Return value

Triangle plane.
## dvec4 TrianglePlane ( dvec3 v0 , dvec3 v1 , dvec3 v2 )

Returns the triangle plane.
### Arguments

- *dvec3* **v0** - The first triangle vertex.
- *dvec3* **v1** - The second triangle vertex.
- *dvec3* **v2** - The third triangle vertex.

### Return value

Triangle plane.
## vec4 TriangleTangent ( vec3 v0 , vec3 v1 , vec3 v2 )

Returns the triangle tangent space.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.

### Return value

Triangle tangent space vector.
## vec4 TriangleTangent ( vec3 v0 , vec3 v1 , vec3 v2 , vec2 t0 , vec2 t1 , vec2 t2 , vec3 normal )

Returns the triangle tangent space.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.
- *vec2* **t0** - Tangent vector of the first triangle vertex.
- *vec2* **t1** - Tangent vector of the second triangle vertex.
- *vec2* **t2** - Tangent vector of the third triangle vertex.
- *vec3* **normal** - Normal.

### Return value

Triangle tangent space vector.
## vec4 TriangleTangent ( vec3 v0 , vec3 v1 , vec3 v2 , vec2 t0 , vec2 t1 , vec2 t2 )

Returns the triangle tangent space.
### Arguments

- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.
- *vec2* **t0** - Tangent vector of the first triangle vertex.
- *vec2* **t1** - Tangent vector of the second triangle vertex.
- *vec2* **t2** - Tangent vector of the third triangle vertex.

### Return value

Triangle tangent space vector.
## dvec4 PolygonPlane ( dvec3[] vertex , int[] indices )

Returns the polygon plane.
### Arguments

- *dvec3[]* **vertex** - Vertex structure.
- *int[]* **indices** - Array of vertex indices.

### Return value

Polygon plane.
## vec4 PolygonPlane ( vec3[] vertex , int[] indices )

Returns the polygon plane.
### Arguments

- *vec3[]* **vertex** - Vertex structure.
- *int[]* **indices** - Array of vertex indices.

### Return value

Polygon plane.
## bool PointTriangleInside ( vec3 point , vec3 v0 , vec3 v1 , vec3 v2 )

Checks if a point is inside a triangle.
### Arguments

- *vec3* **point** - Point to be checked.
- *vec3* **v0** - The first vertex of the triangle.
- *vec3* **v1** - The second vertex of the triangle.
- *vec3* **v2** - The third vertex of the triangle.

### Return value

true if the point is inside the given triangle; otherwise, false.
## bool PointTriangleInside ( dvec3 point , dvec3 v0 , dvec3 v1 , dvec3 v2 )

Checks if a point is inside a triangle.
### Arguments

- *dvec3* **point** - Point to be checked.
- *dvec3* **v0** - The first vertex of the triangle.
- *dvec3* **v1** - The second vertex of the triangle.
- *dvec3* **v2** - The third vertex of the triangle.

### Return value

true if the point is inside the given triangle; otherwise, false.
## bool PointTriangleInside ( vec3 point , vec3 v0 , vec3 v1 , vec3 v2 , vec3 normal )

Checks if a point is inside a triangle.
### Arguments

- *vec3* **point** - Point to be checked.
- *vec3* **v0** - The first vertex of the triangle.
- *vec3* **v1** - The second vertex of the triangle.
- *vec3* **v2** - The third vertex of the triangle.
- *vec3* **normal** - Normal to the triangle plane.

### Return value

true if the point is inside the given triangle; otherwise, false.
## bool PointTriangleInside ( dvec3 point , dvec3 v0 , dvec3 v1 , dvec3 v2 , dvec3 normal )

Checks if a point is inside a triangle.
### Arguments

- *dvec3* **point** - Point to be checked.
- *dvec3* **v0** - The first vertex of the triangle.
- *dvec3* **v1** - The second vertex of the triangle.
- *dvec3* **v2** - The third vertex of the triangle.
- *dvec3* **normal** - Normal to the triangle plane.

### Return value

true if the point is inside the given triangle; otherwise, false.
## float PointTriangleDistance ( vec3 point , vec3 v0 , vec3 v1 , vec3 v2 , vec4 plane )

Returns the closest distance from a point to a triangle.
### Arguments

- *vec3* **point** - Point.
- *vec3* **v0** - The first vertex of the triangle.
- *vec3* **v1** - The second vertex of the triangle.
- *vec3* **v2** - The third vertex of the triangle.
- *vec4* **plane** - Triangle plane.

### Return value

Distance.
## double PointTriangleDistance ( dvec3 point , dvec3 v0 , dvec3 v1 , dvec3 v2 , dvec4 plane )

Returns the closest distance from a point to a triangle.
### Arguments

- *dvec3* **point** - Point.
- *dvec3* **v0** - The first vertex of the triangle.
- *dvec3* **v1** - The second vertex of the triangle.
- *dvec3* **v2** - The third vertex of the triangle.
- *dvec4* **plane** - Triangle plane.

### Return value

Distance.
## void PointTriangleCoordinates ( vec2 point , vec2 v0 , vec2 v1 , vec2 v2 , float a , float b )

Calculates barycentric triangle coordinates. The coordinates will be put to corresponding return variables.
### Arguments

- *vec2* **point** - Point.
- *vec2* **v0** - The first vertex of the triangle.
- *vec2* **v1** - The second vertex of the triangle.
- *vec2* **v2** - The third vertex of the triangle.
- *float* **a** - Return variable.
- *float* **b** - Return variable.

## void PointTriangleCoordinates ( vec3 point , vec3 v0 , vec3 v1 , vec3 v2 , float a , float b )

Calculates barycentric triangle coordinates. The coordinates will be put to corresponding return variables.
### Arguments

- *vec3* **point** - Point.
- *vec3* **v0** - The first vertex of the triangle.
- *vec3* **v1** - The second vertex of the triangle.
- *vec3* **v2** - The third vertex of the triangle.
- *float* **a** - Return variable.
- *float* **b** - Return variable.

## void PointTriangleCoordinates ( dvec3 point , dvec3 v0 , dvec3 v1 , dvec3 v2 , double a , double b )

Calculates barycentric triangle coordinates. The coordinates will be put to corresponding return variables.
### Arguments

- *dvec3* **point** - Point.
- *dvec3* **v0** - The first vertex of the triangle.
- *dvec3* **v1** - The second vertex of the triangle.
- *dvec3* **v2** - The third vertex of the triangle.
- *double* **a** - Return variable.
- *double* **b** - Return variable.

## float PointPolygonDistance ( vec3 point , vec3[] vertex , int[] indices , vec4 plane )

Returns the distance from a point to a polygon.
### Arguments

- *vec3* **point** - Point.
- *vec3[]* **vertex** - Vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *vec4* **plane** - Polygon plane.

### Return value

Distance.
## double PointPolygonDistance ( dvec3 point , dvec3[] vertex , int[] indices , dvec4 plane )

Returns the distance from a point to a polygon.
### Arguments

- *dvec3* **point** - Point.
- *dvec3[]* **vertex** - Vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *dvec4* **plane** - Polygon plane.

### Return value

Distance.
## bool RayBoundBoxIntersection ( vec3 point , vec3 direction , vec3 min , vec3 max )

Checks if a ray intersects a bounding box. The same function as [IRayBoundBoxIntersection()](#IRayBoundBoxIntersection_vec3_vec3_vec3_vec3_bool), but the latter has higher performance due to reduction of division operations, as the ray direction is replaced by the pre-calculated inverse of the ray direction.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec3* **min** - Min coordinates of the axis-aligned bounding box.
- *vec3* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

true if the given ray intersects the given bounding box; otherwise, false.
## bool RayBoundBoxIntersection ( dvec3 point , dvec3 direction , dvec3 min , dvec3 max )

Checks if a ray intersects a bounding box. The same function as [IRayBoundBoxIntersection()](#IRayBoundBoxIntersection_dvec3_dvec3_dvec3_dvec3_bool), but the latter has higher performance due to reduction of division operations, as the ray direction is replaced by the pre-calculated inverse of the ray direction.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec3* **min** - Min coordinates of the axis-aligned bounding box.
- *dvec3* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

true if the given ray intersects the given bounding box; otherwise, false.
## bool IRayBoundBoxIntersection ( vec3 point , vec3 idirection , vec3 min , vec3 max )

Checks if there is an intersection between a ray and a bounding box. The same function as [RayBoundBoxIntersection()](#RayBoundBoxIntersection_vec3_vec3_vec3_vec3_bool), but it uses the inverse of the ray direction, which increases performance.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **idirection** - Inverse direction of the ray.
- *vec3* **min** - Min coordinates of the axis-aligned bounding box.
- *vec3* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

true if the given ray intersects the given bounding box; otherwise, false.
## bool IRayBoundBoxIntersection ( dvec3 point , dvec3 idirection , dvec3 min , dvec3 max )

Checks if there is an intersection between a ray and a bounding box. The same function as [RayBoundBoxIntersection()](#RayBoundBoxIntersection_dvec3_dvec3_dvec3_dvec3_bool), but it uses the inverse of the ray direction, which increases performance.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **idirection** - Inverse direction of the ray.
- *dvec3* **min** - Min coordinates of the axis-aligned bounding box.
- *dvec3* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

true if the given ray intersects the given bounding box; otherwise, false.
## bool RayTriangleIntersection ( vec3 point , vec3 direction , vec3 v0 , vec3 v1 , vec3 v2 )

Checks if a ray intersects a triangle.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec3* **v0** - The first triangle vertex.
- *vec3* **v1** - The second triangle vertex.
- *vec3* **v2** - The third triangle vertex.

### Return value

true if the given ray intersects the given triangle; otherwise, false.
## bool RayTriangleIntersection ( dvec3 point , dvec3 direction , dvec3 v0 , dvec3 v1 , dvec3 v2 )

Checks if a ray intersects a triangle.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec3* **v0** - The first triangle vertex.
- *dvec3* **v1** - The second triangle vertex.
- *dvec3* **v2** - The third triangle vertex.

### Return value

true if the given ray intersects the given triangle; otherwise, false.
## bool LinePlaneIntersection ( vec3 p0 , vec3 p1 , vec4 plane )

Checks if there is an intersection between a line and a plane.
### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec4 plane )

Checks if there is an intersection between a line and a plane.
### Arguments

- *dvec3* **p0** - Start point of the line.
- *dvec3* **p1** - End point of the line.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( vec3 p0 , vec3 p1 , vec3 plane_point , vec3 plane_normal )

Checks if there is an intersection between a line and a plane.
### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *vec3* **plane_point** - Point of the plane.
- *vec3* **plane_normal** - Normal to the plane.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec3 plane_point , dvec3 plane_normal )

Checks if there is an intersection between a line and a plane.
### Arguments

- *dvec3* **p0** - Start point of the line.
- *dvec3* **p1** - End point of the line.
- *dvec3* **plane_point** - Point of the plane.
- *dvec3* **plane_normal** - Normal to the plane.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( vec3 p0 , vec3 p1 , vec4 plane , vec3 ret )

Checks if there is an intersection between a line and a plane.
### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *vec3* **ret** - Return vector.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec4 plane , dvec3 ret )

Checks if there is an intersection between a line and a plane.
### Arguments

- *dvec3* **p0** - Start point of the line.
- *dvec3* **p1** - End point of the line.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *dvec3* **ret** - Return vector.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( vec3 p0 , vec3 p1 , vec3 plane_point , vec3 plane_normal , vec3 ret )

Checks if there is an intersection between a line and a plane.
### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *vec3* **plane_point** - Point of the plane.
- *vec3* **plane_normal** - Normal to the plane.
- *vec3* **ret** - Return vector.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool LinePlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec3 plane_point , dvec3 plane_normal , dvec3 ret )

Checks if there is an intersection between a line and a plane.
### Arguments

- *dvec3* **p0** - Start point of the line.
- *dvec3* **p1** - End point of the line.
- *dvec3* **plane_point** - Point of the plane.
- *dvec3* **plane_normal** - Normal to the plane.
- *dvec3* **ret** - Return vector.

### Return value

true if the given line intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( vec3 point , vec3 direction , vec4 plane )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( dvec3 point , dvec3 direction , dvec4 plane )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( vec3 point , vec3 direction , vec3 plane_point , vec3 plane_normal )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec3* **plane_point** - Point on the plane.
- *vec3* **plane_normal** - Normal to the plane.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( dvec3 point , dvec3 direction , dvec3 plane_point , dvec3 plane_normal )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec3* **plane_point** - Point on the plane.
- *dvec3* **plane_normal** - Normal to the plane.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( vec3 point , vec3 direction , vec4 plane , vec3 ret )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *vec3* **ret** - Return vector.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( dvec3 point , dvec3 direction , dvec4 plane , dvec3 ret )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *dvec3* **ret** - Return vector.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( vec3 point , vec3 direction , vec3 plane_point , vec3 plane_normal , vec3 ret )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction of the ray.
- *vec3* **plane_point** - Point on the plane.
- *vec3* **plane_normal** - Normal to the plane.
- *vec3* **ret** - Return vector.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool RayPlaneIntersection ( dvec3 point , dvec3 direction , dvec3 plane_point , dvec3 plane_normal , dvec3 ret )

Checks if there is an intersection between a ray and a plane.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction of the ray.
- *dvec3* **plane_point** - Point on the plane.
- *dvec3* **plane_normal** - Normal to the plane.
- *dvec3* **ret** - Return vector.

### Return value

true if the given ray intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( vec3 p0 , vec3 p1 , vec4 plane )

Checks if a segment intersects a plane.
### Arguments

- *vec3* **p0** - Starting point of the line segment.
- *vec3* **p1** - End point of the line segment.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec4 plane )

Checks if a segment intersects a plane.
### Arguments

- *dvec3* **p0** - Starting point of the line segment.
- *dvec3* **p1** - End point of the line segment.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( vec3 p0 , vec3 p1 , vec3 plane_point , vec3 plane_normal )

Checks if a segment intersects a plane.
### Arguments

- *vec3* **p0** - Starting point of the line segment.
- *vec3* **p1** - End point of the line segment.
- *vec3* **plane_point** - Point on the plane.
- *vec3* **plane_normal** - Normal to the plane.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec3 plane_point , dvec3 plane_normal )

Checks if a segment intersects a plane.
### Arguments

- *dvec3* **p0** - Starting point of the line segment.
- *dvec3* **p1** - End point of the line segment.
- *dvec3* **plane_point** - Point on the plane.
- *dvec3* **plane_normal** - Normal to the plane.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( vec3 p0 , vec3 p1 , vec4 plane , vec3 ret )

Calculates the intersection of a segment and a plane. If the function returns true, the point of intersection will be put to the return vector.
### Arguments

- *vec3* **p0** - Starting point of the line segment.
- *vec3* **p1** - End point of the line segment.
- *vec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *vec3* **ret** - Return vector.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec4 plane , dvec3 ret )

Calculates the intersection of a segment and a plane. If the function returns true, the point of intersection will be put to the return vector.
### Arguments

- *dvec3* **p0** - Starting point of the line segment.
- *dvec3* **p1** - End point of the line segment.
- *dvec4* **plane** - 4D vector *(A, B, C, D)* representing a plane, where: *A,B,C* are the components of the normal vector of the plane, and *D* is the distance of the plane from the origin.
- *dvec3* **ret** - Return vector.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( vec3 p0 , vec3 p1 , vec3 plane_point , vec3 plane_normal , vec3 ret )

Calculates the intersection of a segment and a plane. If the function returns true, the point of intersection will be put to the return vector.
### Arguments

- *vec3* **p0** - Starting point of the line segment.
- *vec3* **p1** - End point of the line segment.
- *vec3* **plane_point** - Point on the plane.
- *vec3* **plane_normal** - Normal to the plane.
- *vec3* **ret** - Return vector.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## bool SegmentPlaneIntersection ( dvec3 p0 , dvec3 p1 , dvec3 plane_point , dvec3 plane_normal , dvec3 ret )

Calculates the intersection of a segment and a plane. If the function returns true, the point of intersection will be put to the return vector.
### Arguments

- *dvec3* **p0** - Starting point of the line segment.
- *dvec3* **p1** - End point of the line segment.
- *dvec3* **plane_point** - Point on the plane.
- *dvec3* **plane_normal** - Normal to the plane.
- *dvec3* **ret** - Return vector.

### Return value

true if the given segment intersects the given plane; otherwise, false.
## vec3 GetClosestPointOnLine ( vec3 point , vec3 p0 , vec3 p1 )

Scans the specified line segment and returns the point closest to the reference point.
### Arguments

- *vec3* **point** - Reference point.
- *vec3* **p0** - Starting point of the line.
- *vec3* **p1** - End point of the line.

### Return value

Return value.
## dvec3 GetClosestPointOnLine ( dvec3 point , dvec3 p0 , dvec3 p1 )

Scans the specified line segment and returns the point closest to the reference point.
### Arguments

- *dvec3* **point** - Reference point.
- *dvec3* **p0** - Starting point of the line.
- *dvec3* **p1** - End point of the line.

### Return value

Return value.
## bool GetClosestPointOnTriangle ( vec3 point , vec3 v0 , vec3 v1 , vec3 v2 , vec3 ret )

Scans the specified triangle and searches for the point closest to the reference point. The found point will be put to the return vector.
### Arguments

- *vec3* **point** - Reference point.
- *vec3* **v0** - The first vertex of the triangle.
- *vec3* **v1** - The second vertex of the triangle.
- *vec3* **v2** - The third vertex of the triangle.
- *vec3* **ret** - Return vector.

### Return value

true if the point is inside the triangle; otherwise, false.
## bool GetClosestPointOnTriangle ( dvec3 point , dvec3 v0 , dvec3 v1 , dvec3 v2 , dvec3 ret )

Scans the specified triangle and searches for the point closest to the reference point. The found point will be put to the return vector.
### Arguments

- *dvec3* **point** - Reference point.
- *dvec3* **v0** - The first vertex of the triangle.
- *dvec3* **v1** - The second vertex of the triangle.
- *dvec3* **v2** - The third vertex of the triangle.
- *dvec3* **ret** - Return vector.

### Return value

true if the point is inside the triangle; otherwise, false.
## bool GetClosestPointsOnLines ( vec3 p00 , vec3 p01 , vec3 p10 , vec3 p11 , vec3 ret_0 , vec3 ret_1 )

Scans the two specified lines and searches for the pair of closest points. The closest points of the first and the second lines will be put to the respective return vector.
### Arguments

- *vec3* **p00** - Starting point of the first line.
- *vec3* **p01** - End point of the first line.
- *vec3* **p10** - Starting point of the second line.
- *vec3* **p11** - End point of the second line.
- *vec3* **ret_0** - First return vector.
- *vec3* **ret_1** - Second return vector.

### Return value

true if the lines cross; otherwise, false.
## bool GetClosestPointsOnLines ( dvec3 p00 , dvec3 p01 , dvec3 p10 , dvec3 p11 , dvec3 ret_0 , dvec3 ret_1 )

Scans the two specified lines and searches for the pair of closest points. The closest points of the first and the second lines will be put to the respective return vector.
### Arguments

- *dvec3* **p00** - Starting point of the first line.
- *dvec3* **p01** - End point of the first line.
- *dvec3* **p10** - Starting point of the second line.
- *dvec3* **p11** - End point of the second line.
- *dvec3* **ret_0** - First return vector.
- *dvec3* **ret_1** - Second return vector.

### Return value

true if the lines cross; otherwise, false.
## vec3 ProjectOntoPlane ( vec3 v , vec3 plane_normal )

Calculates the projection of a vector onto a given plane.
### Arguments

- *vec3* **v** - Input vector.
- *vec3* **plane_normal** - Normal to the plane.

### Return value

Projection of the input vector onto the plane.
## dvec3 ProjectOntoPlane ( dvec3 v , dvec3 plane_normal )

Calculates the projection of a vector onto a given plane.
### Arguments

- *dvec3* **v** - Input vector.
- *dvec3* **plane_normal** - Normal to the plane.

### Return value

Projection of the input vector onto the plane.
## void TriangleRasterize ( vec2 v0 , vec2 v1 , vec2 v2 , int x0 , int y0 , int x1 , int y1 , TriangleRasterizeShader shader )

Positions the given triangle within the given screen coordinates, rasterizes it and applies the specified shader to each pixel.
### Arguments

- *vec2* **v0** - The first vertex of the triangle.
- *vec2* **v1** - The second vertex of the triangle.
- *vec2* **v2** - The third vertex of the triangle.
- *int* **x0** - The X coordinate of the top left corner of screen space.
- *int* **y0** - The Y coordinate of the top left corner of screen space.
- *int* **x1** - The X coordinate of the bottom right corner of screen space.
- *int* **y1** - The Y coordinate of the bottom right corner of screen space.
- *TriangleRasterizeShader* **shader** - Shader.
