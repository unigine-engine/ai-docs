# Unigine::BoundBox Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding box in single precision coordinates.


> **Notice:** Instances of this structure are deleted automatically when it is necessary.


In case of double precision coordinates, the bounding box should be constructed by using the **[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)** structure.  It includes the same functions as the *BoundBox* structure, but its functions deal with the double precision coordinates.


> **Notice:** To support both single and double precision builds, you can use the *WorldBoundBox* structure only. The engine will automatically substitute it with the *BoundBox* if it is required.


## BoundBox Class

### Members

---

## BoundBox ( )

Constructor. Creates an empty bounding box.
## BoundBox ( const BoundBox& bb )

Constructor. Initialization by the bounding box.
### Arguments

- *const BoundBox&* **bb** - Bounding box.

## explicit BoundBox ( const BoundSphere & bs )

Constructor. Initialization by the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

## BoundBox ( const BoundBox & bb , const mat4 & transform )

Constructor. Initialization by the bounding box with the transformation matrix taken into account.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *const [mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## BoundBox ( const Math:: vec3 * points , int num_points )

Constructor. Initialization by the vector of points.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## BoundBox ( const vec3 & minimum , const vec3 & maximum )

Constructor. Initialization by minimum and maximum coordinates of the bounding box.
### Arguments

- *const [vec3](../../../../api/library/math/class.vec3_cpp.md) &* **minimum** - Bounding box minimum coordinates.
- *const [vec3](../../../../api/library/math/class.vec3_cpp.md) &* **maximum** - Bounding box maximum coordinates.

## BoundBox ( float x_min , float y_min , float z_min , float x_max , float y_max , float z_max )

Constructor. Initialization by minimum and maximum coordinates of the bounding box specified as float values.
### Arguments

- *float* **x_min** - Minimum X-coordinate of the bounding box.
- *float* **y_min** - Minimum Y-coordinate of the bounding box.
- *float* **z_min** - Minimum Y-coordinate of the bounding box.
- *float* **x_max** - Maximum X-coordinate of the bounding box.
- *float* **y_max** - Maximum Y-coordinate of the bounding box.
- *float* **z_max** - Maximum Z-coordinate of the bounding box.

## vec3 getSize ( ) const

Returns the size of the bounding box along the axes.
### Return value

Vector containing sizes of the bounding box along the axes, in units.
## void clear ( )

Clears the bounding box.
## void set ( const Math:: vec3 & min_ , const Math:: vec3 & max )

Sets the bounding box by its minimum and maximum coordinates.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min_** - Minimum coordinates of the bounding box.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - Maximum coordinates of the bounding box.

## void set ( const Math:: vec3 * points , int num_points )

Sets the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - List of points to be enclosed by the bounding box.
- *int* **num_points** - Number of points to be enclosed by the bounding box.

## void set ( const BoundSphere & bs )

Sets the bounding box by the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

## void set ( const BoundBox & bb )

Sets the bounding box equal to the specified source bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Source bounding box.

## void set ( const BoundBox & bb , const Math:: mat4 & transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const Math:: mat4 & transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const Math:: dmat4 & transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const BoundSphere & bs , const Math:: mat4 & transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const BoundSphere & bs , const Math:: dmat4 & transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.
- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **transform** - Transformation matrix.

## int compare ( const BoundBox & bb ) const

Compares the current bounding box with the given one.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box to compare with.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## BoundBox & operator= ( const BoundBox & bb )

Assignment operator for the bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

Bounding box.
## int operator== ( const BoundBox& bb ) const

Compares the current bounding box with the given one.
### Arguments

- *const BoundBox&* **bb** - The bounding box to compare with.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## int operator!= ( const BoundBox & bb ) const

Bounding boxes not equal comparison operator.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box to compare with.

### Return value

**true** if the size and position of both bounding boxes are not equal; otherwise, **false**.
## BoundBox operator* ( const mat4 & m , const BoundBox & bb )

Returns the bounding box with the specified transformation matrix applied.
### Arguments

- *const [mat4](../../../../api/library/math/class.mat4_cpp.md) &* **m** - Transform matrix.
- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

The bounding box with the specified transform.
## BoundBox operator* ( const dmat4 & m , const BoundBox & bb )

Returns the bounding box with the specified transformation matrix applied.
### Arguments

- *const [dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **m** - Transform matrix.
- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

The bounding box with the specified transform.
## void expand ( const Math:: vec3 & point )

Expands the current bounding box to enclose the given point.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.

## void expand ( const Math:: vec3 * points , int num_points )

Expands the current bounding box to enclose all given points.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - List of points to be enclosed by the bounding box.
- *int* **num_points** - Number of points to be enclosed by the bounding box.

## void expand ( const BoundSphere & bs )

Expands the current bounding box to enclose the given bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

## void expand ( const BoundBox & bb )

Expands the current bounding box to enclose the given bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## bool inside ( const Math:: vec3 & point ) const

Checks if the given point is inside the bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool inside ( const Math:: vec3 & point , float radius ) const

Checks if the given sphere is inside the current bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the center of the sphere.
- *float* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool inside ( const Math:: vec3 & minimum , const Math:: vec3 & maximum ) const

Checks if the box with the given coordinates is inside the current bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **minimum** - Minimum coordinates of the box.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **maximum** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool inside ( const BoundSphere & bs ) const

Checks if the specified bounding sphere is inside the current bounding box.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool inside ( const BoundBox & bb ) const

Checks if the specified bounding box is inside the current bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & point ) const


Checks if the given point is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool insideValid ( const vec3* points , int num_points ) const


Checks if any of the given points is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const vec3** **points** - Array of points to be checked.
- *int* **num_points** - Number of points to be checked.

### Return value

**true** if any of the given points is inside the bounding box; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & point , float radius ) const


Checks if the sphere is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the center of the sphere.
- *float* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & min_ , const Math:: vec3 & max_ ) const


Checks if the box is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min_** - Box minimum coordinates.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max_** - Box maximum coordinates.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool insideValid ( const BoundSphere & bs ) const


Checks if the bounding sphere is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool insideValid ( const BoundBox & bb ) const


Checks if the bounding box is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool insideAll ( const BoundSphere & bs ) const

Checks if the whole given bounding sphere is inside the current bounding box.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool insideAll ( const BoundBox & bb ) const

Checks if the whole given bounding box is inside the current bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool insideAllValid ( const BoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool insideAllValid ( const BoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool insideAllValid ( const vec3* points , int num_points ) const


Checks if all specified points are inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const vec3** **points** - Array of points to be checked.
- *int* **num_points** - Number of points to be checked.

### Return value

**true** if the all specified points are inside the bounding box; otherwise, **false**.
## bool insideCube ( int face , const Math:: vec3 & offset ) const

Checks if a face of the current bounding box is inside the cube represented by minimum and maximum coordinates of the bounding box.
### Arguments

- *int* **face** - The face index from **0** to **5**.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **offset** - Offset.

### Return value

**true** if the face is inside the bounding cube; otherwise, **false**.
## bool rayIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction ) const

Checks for an intersection between a ray and the current bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction vector of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool irayIntersection ( const Math:: vec3 & point , const Math:: vec3 & idirection ) const

Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool getIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 ) const

Checks for an intersection between a line and the current bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Enging point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## bool rayIntersectionValid ( const Math:: vec3 & point , const Math:: vec3 & direction ) const


Checks for an intersection between a ray and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction vector of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool irayIntersectionValid ( const Math:: vec3 & point , const Math:: vec3 & idirection ) const


Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool getIntersectionValid ( const Math:: vec3 & p0 , const Math:: vec3 & p1 ) const


Checks for an intersection between a line and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Enging point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## float distance ( ) const

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance in units, if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../api/library/math/constants_cpp.md)**.
## float distance ( const Math:: vec3 & point ) const

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of a point.

### Return value

Distance, in units.
## float distanceValid ( ) const

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance, in units.
## float distanceValid ( const Math:: vec3 & point ) const

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

Distance, in units.
## void getPoints ( vec3 * points , int num_points ) const

Puts the vertices of the current bounding box into the given vector.
### Arguments

- *[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Target vector.
- *int* **num_points** - Number of points, must be equal to 8.

## void getPlanes ( vec4 * planes , int num_planes ) const

Puts the planes created based on the vertices of the current bounding box into the given vector.
### Arguments

- *[vec4](../../../../api/library/math/class.vec4_cpp.md) ** **planes** - Target vector.
- *int* **num_planes** - Number of planes, must be equal to 6.

## vec3 getCenter ( ) const

Returns the center point of the current bounding box.
### Return value

Center point.
## bool isValid ( ) const

Checks the bounding box status.
### Return value

**true** if the bounding box minimum and maximum coordinates are valid; otherwise, **false**.
## bool isCameraVisible ( const vec3& camera , float min_distance , float max_distance ) const

Returns a value indicating if the bounding box bounding box is within the camera visibility distance.
### Arguments

- *const vec3&* **camera** - Coordinates of the camera position.
- *float* **min_distance** - Minimum visibility distance, in meters.
- *float* **max_distance** - Maximum visibility distance, in meters.

### Return value

**true** if the bounding box is within the camera visibility distance; otherwise, **false**.
