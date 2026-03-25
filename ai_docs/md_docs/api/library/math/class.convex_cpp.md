# Unigine::Convex Class (CPP)

**Header:** #include <UnigineMathLibConvex.h>


This class creates convex shapes.


## Convex Class

### Members

---

## static ConvexPtr create ( )

Constructor. Initializes the new convex shape by clearing data of the prevoius shape.
## static ConvexPtr create ( const Convex& convex )

Constructor. Initializes the new convex shape using the given shape.
### Arguments

- *const Convex&* **convex** - Input convex shape.

## Convex & operator= ( const Convex& convex )

Sets the convex shape to be equal the given convex shape.
### Arguments

- *const Convex&* **convex** - Convex shape.

### Return value

Resulting convex shape.
## void clear ( )

Clears the data of the prevoius convex shape.
## bool create ( const vec3* v , int num_vertex , float error = 0.01f )

Creates the convex shape using the given vertices.
### Arguments

- *const vec3** **v** - Vertices.
- *int* **num_vertex** - Number of vertices.
- *float* **error** - Approximation error (value in range **[0..1]**, a higher value mean fewer vertices). This value allows reducing the number of vertices of the created shape. Convex hulls with fewer vertices are processed faster.

### Return value

true if the shape was successfully created; otherwise false.
## bool create ( const dvec3* v , int num_vertex , float error = 0.01f )

Creates the convex shape using the given vertices.
### Arguments

- *const dvec3** **v** - Vertices.
- *int* **num_vertex** - Number of vertices.
- *float* **error** - Approximation error (value in range **[0..1]**, a higher value mean fewer vertices). This value allows reducing the number of vertices of the created shape. Convex hulls with fewer vertices are processed faster.

### Return value

true if the shape was successfully created; otherwise false.
## int getNumVertex ( ) const

Returns the number of vertices the convex shape consists of.
### Return value

Number of vertices.
## const dvec3 * getVertex ( ) const

Returns the pointer to the array of vertices for the convex shape.
### Return value

Pointer to the array of vertices.
## const dvec3 & getVertex ( int num ) const

Returns the vertex with the given number.
### Arguments

- *int* **num** - Number of the vertex.

### Return value

Resulting vertex.
## int getNumFaces ( ) const

Returns the number of faces for this convex shape.
### Return value

Number of faces.
## int getNumFaceVertex ( int face ) const

Returns the number of vertices for the given face.
### Arguments

- *int* **face** - Number of the face.

### Return value

Number of vertices.
## int getFaceVertex ( int face , int num ) const

Returns the specified vertex of the specified face.
### Arguments

- *int* **face** - Face of the convex shape.
- *int* **num** - Number of the vertex.

### Return value

Index of the vertex.
## double getVolume ( ) const

Returns the convex shape's volume.
### Return value

Convex shape's volume.
## double getThreshold ( ) const

Returns the merge threshold.
### Return value

Merge threshold.
## dvec3 getCenter ( ) const

Returns the center of the convex shape.
### Return value

Center of the convex shape.
## mat3 getInertia ( ) const

Returns the inertia matrix.
### Return value

Inertia matrix.
## dvec3 getClosestPoint ( const dvec3& point ) const

Returns the closest convex shape's point to the given point.
### Arguments

- *const dvec3&* **point** - Given point.

### Return value

Closest point (inside or on the edge of the convex shape).
## void getBoundBox ( dvec3& min , dvec3& max ) const

Calculates the convex shape's bounding box (minimum and maximum vertices).
### Arguments

- *dvec3&* **min** - Minimum vertex of the shape.
- *dvec3&* **max** - Maximum vertex of the shape.
