# Unigine::Concave Class (CPP)

**Header:** #include <UnigineMathLibConcave.h>


This class creates concave shapes based on vertices by using a subset of convex shapes.


## Concave Class

### Members

---

## static ConcavePtr create ( )

Constructor. Initializes the new concave shape by clearing data of the prevoius concave shape.
## static ConcavePtr create ( const Concave& concave )

Constructor. Initializes the new concave shape using the given shape.
### Arguments

- *const Concave&* **concave** - Input concave shape.

## Concave & operator= ( const Concave& concave )

Sets the concave shape to be equal the given concave shape.
### Arguments

- *const Concave&* **concave** - Concave shape.

### Return value

Resulting concave shape.
## void clear ( )

Clears the data of the prevoius concave shape.
## bool create ( const vec3* vertex_ , int num_vertex_ , int depth_ = 4 , float error_ = 0.01f , float threshold_ = 0.01f )

Creates the concave shape using the given vertices.
### Arguments

- *const vec3** **vertex_** - Vertices.
- *int* **num_vertex_** - Number of vertices.
- *int* **depth_** - Recursion depth.
- *float* **error_** - Convex error.
- *float* **threshold_** - Merge threshold.

### Return value

true if the shape was successfully created; otherwise false.
## float getError ( ) const

Returns the convex error.
## float getThreshold ( ) const

Returns the merge threshold.
## int getNumConvexes ( ) const

Returns the number of convex hulls used to create this concave shape.
### Return value

Number of convex hulls.
## const Convex * getConvex ( int num ) const

Returns the convex shape that is a part of this concave shape.
### Arguments

- *int* **num** - Number of the convex shape.

### Return value

Convex shape.
