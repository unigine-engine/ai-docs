# Unigine::Polygon Class (CPP)

**Header:** #include <UnigineMathLibPolygon.h>


This class creates an indexed polygon (convex or concave) using vertices and a plane normal.


## Polygon Class

### Members

---

## void clear ( )

Clears the data (vertices and indices) of the polygon.
## bool createConvex ( const vec3* v , int num_vertex , const vec3& normal )

Creates the convex polygon.
### Arguments

- *const vec3** **v** - Pointer to an array of vertices.
- *int* **num_vertex** - Number of vertices. > **Notice:** Must be greater than or equal to 3.
- *const vec3&* **normal** - Normal of the polygon.

### Return value

true if the convex polygon was successfully created; otherwise false.
## bool createConvex ( const Vector < vec3 >& v , const vec3& normal )

Creates the convex polygon.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec3](../../../api/library/math/class.vec3_cpp.md)>&* **v** - Vector of polygon vertices.
- *const vec3&* **normal** - Normal of the polygon.

### Return value

true if the convex polygon was successfully created; otherwise false.
## bool createConcave ( const vec3* v , int num_vertex , const vec3& normal )

Creates the concave polygon.
### Arguments

- *const vec3** **v** - Pointer to an array of vertices.
- *int* **num_vertex** - Number of vertices. > **Notice:** Must be greater than or equal to 3.
- *const vec3&* **normal** - Normal of the polygon.

### Return value

true if the concave polygon was successfully created; otherwise false.
## bool createConcave ( const Vector < vec3 >& v , const vec3& normal )

Creates the concave polygon.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec3](../../../api/library/math/class.vec3_cpp.md)>&* **v** - Vector of polygon vertices.
- *const vec3&* **normal** - Normal of the polygon.

### Return value

true if the concave polygon was successfully created; otherwise false.
## int getNumVertex ( ) const

Returns the number of vertices.
### Return value

Number of vertices.
## const vec3 & getVertex ( int num ) const

Returns the vertex with the given number.
### Arguments

- *int* **num** - Number of the vertex.

### Return value

Resulting vertex.
## int getVertexIndex ( int num ) const

Returns the index of the vertex with the given number.
### Arguments

- *int* **num** - Number of the vertex.

### Return value

Index of the vertex.
## int getNumIndices ( ) const

Returns the number of indices.
### Return value

Number of indices.
## int getIndex ( int num ) const

Returns the index with a given number.
### Arguments

- *int* **num** - Number of the index.

### Return value

Resulting index.
