# Unigine::Geometry Class (CPP)

**Header:** #include <UnigineMathLibGeometry.h>


This class is used to represent a collection of generic 3d math functions such as line plane intersection, closest points on two lines, etc.


## Geometry Class

### Members

---

## void getClosestPointOnLine ( const Math:: dvec3 & point , const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , Math:: dvec3 & ret )

Scans the specified line segment and searches for the point closest to the reference point. The found point is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Reference point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Line start point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - Line end point.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

## void getClosestPointOnLine ( const Math:: vec3 & point , const Math:: vec3 & p0 , const Math:: vec3 & p1 , Math:: vec3 & ret )

Scans the specified line segment and searches for the point closest to the reference point. The found point is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Reference point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

## bool getClosestPointOnTriangle ( const Math:: dvec3 & point , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 , Math:: dvec3 & ret )

Scans the specified triangle and searches for the point closest to the reference point. The found point is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Reference point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the point is inside the triangle; otherwise, **false**
## bool getClosestPointOnTriangle ( const Math:: vec3 & point , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , Math:: vec3 & ret )

Scans the specified triangle and searches for the point closest to the reference point. The found point is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Reference point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the point is inside the triangle; otherwise, **false**
## bool getClosestPointsOnLines ( const Math:: dvec3 & p00 , const Math:: dvec3 & p01 , const Math:: dvec3 & p10 , const Math:: dvec3 & p11 , Math:: dvec3 & ret_0 , Math:: dvec3 & ret_1 )

Scans the two specified lines and searches for the pair of closest points. The closest points of the first and the second lines are put in the respective return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p00** - Start point of the first line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p01** - End point of the first line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p10** - Start point of the second line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p11** - End point of the second line.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_0** - First return vector.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_1** - Second return vector.

### Return value

**true** if the lines cross; otherwise, **false**
## bool getClosestPointsOnLines ( const Math:: vec3 & p00 , const Math:: vec3 & p01 , const Math:: vec3 & p10 , const Math:: vec3 & p11 , Math:: vec3 & ret_0 , Math:: vec3 & ret_1 )

Scans the two specified lines and searches for the pair of closest points. The closest points of the first and the second lines are put in the respective return vectors.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p00** - Start point of the first line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p01** - End point of the first line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p10** - Start point of the second line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p11** - End point of the second line.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_0** - First return vector.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_1** - Second return vector.

### Return value

**true** if the lines cross; otherwise, **false**
## bool irayBoundBoxIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & idirection , const Math:: dvec3 & min , const Math:: dvec3 & max )

Checks if there is an intersection between a ray and a bounding box. The same function as [rayBoundBoxIntersection()](#rayBoundBoxIntersection_dvec3_dvec3_dvec3_dvec3_bool), but it uses the inverse of the ray direction, which increases performance.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **idirection** - Inverse direction of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **min** - Min coordinates of the axis-aligned bounding box.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

**true** if the given ray intersects the given bounding box; otherwise, **false**.
## bool irayBoundBoxIntersection ( const Math:: vec3 & point , const Math:: vec3 & idirection , const Math:: vec3 & min , const Math:: vec3 & max )

Checks if there is an intersection between a ray and a bounding box. The same function as [rayBoundBoxIntersection()](#rayBoundBoxIntersection_vec3_vec3_vec3_vec3_bool), but it uses the inverse of the ray direction, which increases performance.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **idirection** - Inverse direction of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **min** - Min coordinates of the axis-aligned bounding box.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

**true** if the given ray intersects the given bounding box; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec4 & plane )

Checks if there is an intersection between a line and a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec4 & plane )

Checks if there is an intersection between a line and a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal )

Checks if there is an intersection between a line and a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point of the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal )

Checks if there is an intersection between a line and a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - Start point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point of the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec4 & plane , Math:: vec3 & ret )

Calculates the intersection of a line and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec4 & plane , Math:: dvec3 & ret )

Calculates the intersection of a line and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal , Math:: vec3 & ret )

Calculates the intersection of a line and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point of the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## bool linePlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal , Math:: dvec3 & ret )

Calculates the intersection of a line and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point of the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given line intersects the given plane; otherwise, **false**.
## void orthoBasis ( const Math:: vec3 & v , Math:: vec3 & tangent , Math:: vec3 & binormal )

Creates an ortho transformation. Output tangent and binormal vectors are put in corresponding return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Input vector.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **tangent** - Return vector.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **binormal** - Return vector.

## void orthoBasis ( const Math:: dvec3 & v , Math:: dvec3 & tangent , Math:: dvec3 & binormal )

Creates an ortho transformation. Output tangent and binormal vectors are put in corresponding return vectors.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Input vector.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **tangent** - Return vector.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **binormal** - Return vector.

## Math:: quat orthoTangent ( const Math:: vec3 & tangent , const Math:: vec3 & binormal , const Math:: vec3 & normal )

Creates the ortho triangle tangent space basis.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **tangent** - Tangent vector.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **binormal** - Binormal vector.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal vector.

### Return value

Tangent basis.
## Math:: quat orthoTangent ( const Math:: vec4 & tangent , const Math:: vec3 & normal )

Creates the ortho triangle tangent space basis.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **tangent** - Tangent vector.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal vector.

### Return value

Tangent basis.
## void orthoTransform ( const Math:: dvec3 & v , Math:: dmat4 & transform )

Creates an ortho transformation. The transformation is put in the return matrix.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Input vector.
- *Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **transform** - Return matrix.

## void orthoTransform ( const Math:: vec3 & v , Math:: mat4 & transform )

Creates an ortho transformation. The transformation is put in the return matrix.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Input vector.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Return matrix.

## float pointPolygonDistance ( const Math:: vec3 & point , const Math:: vec3 * vertex , int[] indices , int num_indices , const Math:: vec4 & plane )

Returns the distance from a point to a polygon.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Polygon plane.

### Return value

Distance.
## double pointPolygonDistance ( const Math:: dvec3 & point , const Math:: dvec3 * vertex , int[] indices , int num_indices , const Math:: dvec4 & plane )

Returns the distance from a point to a polygon.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Polygon plane.

### Return value

Distance.
## float pointPolygonDistance ( const Math:: vec3 & point , const Math:: vec3 * vertex , unsigned short [] indices , int num_indices , const Math:: vec4 & plane )

Returns the distance from a point to a polygon.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Polygon plane.

### Return value

Distance.
## double pointPolygonDistance ( const Math:: dvec3 & point , const Math:: dvec3 * vertex , unsigned short [] indices , int num_indices , const Math:: dvec4 & plane )

Returns the distance from a point to a polygon.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Polygon plane.

### Return value

Distance.
## bool pointPolygonInside ( const Math:: vec3 & point , const Math:: vec3 * vertex , int[] indices , int num_indices , const Math:: vec3 & normal )

Checks if a point is inside a polygon.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal to the polygon plane.

### Return value

**true** if the point is inside the given polygon; otherwise, **false**.
## bool pointPolygonInside ( const Math:: dvec3 & point , const Math:: dvec3 * vertex , int[] indices , int num_indices , const Math:: dvec3 & normal )

Checks if a point is inside a polygon.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **normal** - Normal to the polygon plane.

### Return value

**true** if the point is inside the given polygon; otherwise, **false**.
## bool pointPolygonInside ( const Math:: vec3 & point , const Math:: vec3 * vertex , unsigned short [] indices , int num_indices , const Math:: vec3 & normal )

Checks if a point is inside a polygon.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal to the polygon plane.

### Return value

**true** if the point is inside the given polygon; otherwise, **false**.
## bool pointPolygonInside ( const Math:: dvec3 & point , const Math:: dvec3 * vertex , unsigned short [] indices , int num_indices , const Math:: dvec3 & normal )

Checks if a point is inside a polygon.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **normal** - Normal to the polygon plane.

### Return value

**true** if the point is inside the given polygon; otherwise, **false**.
## void pointTriangleCoordinates ( const Math:: vec2 & point , const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec2 & v2 , float & a , float & b )

Calculates barycentric triangle coordinates. The coordinates are put in corresponding return variables.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - Point.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - The third vertex of the triangle.
- *float &* **a** - Return variable.
- *float &* **b** - Return variable.

## void pointTriangleCoordinates ( const Math:: vec3 & point , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , float & a , float & b )

Calculates barycentric triangle coordinates. The coordinates are put in corresponding return variables.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *float &* **a** - Return variable.
- *float &* **b** - Return variable.

## void pointTriangleCoordinates ( const Math:: dvec3 & point , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 , double & a , double & b )

Calculates barycentric triangle coordinates. The coordinates are put in corresponding return variables.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *double &* **a** - Return variable.
- *double &* **b** - Return variable.

## double pointTriangleDistance ( const Math:: dvec3 & point , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 , const Math:: dvec4 & plane )

Returns the closest distance from a point to a triangle.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Triangle plane.

### Return value

Distance.
## float pointTriangleDistance ( const Math:: vec3 & point , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , const Math:: vec4 & plane )

Returns the closest distance from a point to a triangle.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Triangle plane.

### Return value

Distance.
## bool pointTriangleInside ( const Math:: vec3 & point , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , const Math:: vec3 & normal )

Checks if a point is inside a triangle.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal to the triangle plane.

### Return value

**true** if the point is inside the given triangle; otherwise, **false**.
## bool pointTriangleInside ( const Math:: dvec3 & point , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 , const Math:: dvec3 & normal )

Checks if a point is inside a triangle.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **normal** - Normal to the triangle plane.

### Return value

**true** if the point is inside the given triangle; otherwise, **false**.
## bool pointTriangleInside ( const Math:: dvec3 & point , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 )

Checks if a point is inside a triangle.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Point.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third vertex of the triangle.

### Return value

**true** if the point is inside the given triangle; otherwise, **false**.
## bool pointTriangleInside ( const Math:: vec3 & point , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Checks if a point is inside a triangle.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vertex of the triangle.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third vertex of the triangle.

### Return value

**true** if the point is inside the given triangle; otherwise, **false**.
## Math:: vec4 polygonPlane ( const Math:: vec3 * vertex , int[] indices , int num_indices )

Returns the polygon plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.

### Return value

Polygon plane.
## Math:: dvec4 polygonPlane ( const Math:: dvec3 * vertex , int[] indices , int num_indices )

Returns the polygon plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *int[]* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.

### Return value

Polygon plane.
## Math:: vec4 polygonPlane ( const Math:: vec3 * vertex , unsigned short [] indices , int num_indices )

Returns the polygon plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.

### Return value

Polygon plane.
## Math:: dvec4 polygonPlane ( const Math:: dvec3 * vertex , unsigned short [] indices , int num_indices )

Returns the polygon plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) ** **vertex** - Pointer to vertex structure.
- *unsigned short []* **indices** - Array of vertex indices.
- *int* **num_indices** - Total number of vertex indices.

### Return value

Polygon plane.
## Math:: vec3 projectOntoPlane ( const Math:: vec3 & v , const Math:: vec3 & plane_normal )

Calculates the projection of a vector onto a given plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Input vector.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

Projection of the input vector onto the plane.
## Math:: dvec3 projectOntoPlane ( const Math:: dvec3 & v , const Math:: dvec3 & plane_normal )

Calculates the projection of a vector onto a given plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Input vector.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

Projection of the input vector onto the plane.
## bool rayBoundBoxIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec3 & min , const Math:: dvec3 & max )

Checks if a ray intersects a bounding box. The same function as [irayBoundBoxIntersection()](#irayBoundBoxIntersection_dvec3_dvec3_dvec3_dvec3_bool), but the latter has higher performance due to reduction of division operations, as the ray direction is replaced by the pre-calculated inverse of the ray direction.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **min** - Min coordinates of the axis-aligned bounding box.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

**true** if the given ray intersects the given bounding box; otherwise, **false**.
## bool rayBoundBoxIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec3 & min , const Math:: vec3 & max )

Checks if a ray intersects a bounding box. The same function as [irayBoundBoxIntersection()](#irayBoundBoxIntersection_vec3_vec3_vec3_vec3_bool), but the latter has higher performance due to reduction of division operations, as the ray direction is replaced by the pre-calculated inverse of the ray direction.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **min** - Min coordinates of the axis-aligned bounding box.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **max** - Max coordinates of the axis-aligned bounding box.

### Return value

**true** if the given ray intersects the given bounding box; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec4 & plane )

Checks if a ray intersects a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec4 & plane )

Checks if a ray intersects a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal )

Checks if a ray intersects a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal )

Checks if a ray intersects a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec4 & plane , Math:: vec3 & ret )

Calculates the intersection of a ray and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec4 & plane , Math:: dvec3 & ret )

Calculates the intersection of a ray and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal , Math:: vec3 & ret )

Calculates the intersection of a ray and a plane. If the function returns **true**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayPlaneIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal , Math:: dvec3 & ret )

Calculates the intersection of a ray and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given ray intersects the given plane; otherwise, **false**.
## bool rayTriangleIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction , const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Checks if a ray intersects a triangle.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

**true** if the given ray intersects the given triangle; otherwise, **false**.
## bool rayTriangleIntersection ( const Math:: dvec3 & point , const Math:: dvec3 & direction , const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 )

Checks if a ray intersects a triangle.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **direction** - Direction of the ray.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

**true** if the given ray intersects the given triangle; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec4 & plane )

Checks if a segment intersects a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec4 & plane )

Checks if a segment intersects a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal )

Checks if a segment intersects a plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal )

Checks if a segment intersects a plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec4 & plane , Math:: vec3 & ret )

Calculates the intersection of a segment and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - Plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec4 & plane , Math:: dvec3 & ret )

Calculates the intersection of a line segment and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **plane** - Plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 , const Math:: vec3 & plane_point , const Math:: vec3 & plane_normal , Math:: vec3 & ret )

Calculates the intersection of a line segment and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## bool segmentPlaneIntersection ( const Math:: dvec3 & p0 , const Math:: dvec3 & p1 , const Math:: dvec3 & plane_point , const Math:: dvec3 & plane_normal , Math:: dvec3 & ret )

Calculates the intersection of a line segment and a plane. If the function returns **1**, the point of intersection is put in the return vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p0** - Start point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **p1** - End point of the line segment.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_point** - Point on the plane.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **plane_normal** - Normal to the plane.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Return vector.

### Return value

**true** if the given segment intersects the given plane; otherwise, **false**.
## double triangleArea ( const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 )

Returns the triangle area.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle area.
## float triangleArea ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Returns the triangle area.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle area.
## Math:: dvec3 triangleNormal ( const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 )

Returns the triangle normal vector.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle normal vector.
## Math:: vec3 triangleNormal ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Returns the triangle normal vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle normal vector.
## Math:: vec4 trianglePlane ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Returns the triangle plane.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle plane.
## Math:: dvec4 trianglePlane ( const Math:: dvec3 & v0 , const Math:: dvec3 & v1 , const Math:: dvec3 & v2 )

Returns the triangle plane.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle plane.
## Math:: vec4 triangleTangent ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , const Math:: vec2 & t0 , const Math:: vec2 & t1 , const Math:: vec2 & t2 )

Returns the triangle tangent space.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t0** - Tangent vector of the first triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t1** - Tangent vector of the second triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t2** - Tangent vector of the third triangle vertex.

### Return value

Triangle tangent space vector.
## Math:: vec4 triangleTangent ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 , const Math:: vec2 & t0 , const Math:: vec2 & t1 , const Math:: vec2 & t2 , const Math:: vec3 & normal )

Returns the triangle tangent space.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t0** - Tangent vector of the first triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t1** - Tangent vector of the second triangle vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **t2** - Tangent vector of the third triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal.

### Return value

Triangle tangent space vector.
## Math:: vec4 triangleTangent ( const Math:: vec3 & v0 , const Math:: vec3 & v1 , const Math:: vec3 & v2 )

Returns the triangle tangent space.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second triangle vertex.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - The third triangle vertex.

### Return value

Triangle tangent space vector.
## void TriangleRasterize ( Vertex * vertex , int x0 , int y0 , int x1 , int y1 , Shader & shader )

Positions the given triangle within the given screen coordinates, rasterizes it and applies the specified shader to each pixel.
### Arguments

- *Vertex ** **vertex** - Pointer to vertex structure.
- *int* **x0** - The X coordinate of the top left corner of screen space.
- *int* **y0** - The Y coordinate of the top left corner of screen space.
- *int* **x1** - The X coordinate of the bottom right corner of screen space.
- *int* **y1** - The Y coordinate of the bottom right corner of screen space.
- *[Shader](../../../api/library/rendering/class.shader_cpp.md) &* **shader** - Shader.
