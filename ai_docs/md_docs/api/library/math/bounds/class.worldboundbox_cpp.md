# Unigine::WorldBoundBox Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding box in double precision coordinates.


Bounding boxes has better precision quality but it takes more time for calculation in comparison with bounding spheres.


By using this structure you can easily find the common bounding box for several objects by expanding the bounding box.


## WorldBoundBox Class

### Members

---

## static WorldBoundBoxPtr create ( )

Default constructor. Creates an empty bounding box.
## WorldBoundBox ( const Math:: Vec3 & min , const Math:: Vec3 & max )

Constructor. Initializes new bounding box by minimum and maximum coordinates of the bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The bounding box minimum coordinates.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The bounding box maximum coordinates.

## BoundBox ( const Math:: Vec3 * points , int num_points )

Constructor. Initialization by the vector of points.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## WorldBoundBox ( const WorldBoundBox & bb )

Constructor. Initializes new bounding box by using given bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.

## WorldBoundBox ( const WorldBoundBox & bb , const Math:: Mat4 & transform )

Constructor. Initialization by the bounding box with the transformation matrix taken into account.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## WorldBoundBox ( const BoundBox & bb )

Constructor. Initializes new bounding box by using given bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## WorldBoundBox ( const BoundBox & bb , const Math:: Mat4 & transform )

Constructor. Initialization by the bounding box with the transformation matrix taken into account.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## WorldBoundBox ( const WorldBoundSphere & bs )

Constructor. Initializes new bounding box by the using given bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.

## WorldBoundBox & operator= ( const WorldBoundBox & bb )

Assignment operator for the bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.

### Return value

Bounding box.
## void clear ( )

Clears the bounding box.
## void set ( const Math:: Vec3 & min , const Math:: Vec3 & max )

Sets the bounding box by its minimum and maximum coordinates.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - Minimum coordinates of the bounding box.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - Maximum coordinates of the bounding box.

## void set ( const Math:: Vec3 * points , int num_points )

Sets the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - List of points to be enclosed by the bounding box.
- *int* **num_points** - Number of points to be enclosed by the bounding box.

## void set ( const WorldBoundSphere & bs )

Sets the bounding box by the bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## void set ( const WorldBoundBox & bb )

Sets the bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

## void set ( const WorldBoundBox & bb , const Math:: Mat4 & transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void set ( const BoundBox & bb )

Sets the bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

## void set ( const BoundBox & bb , const Math:: Mat4 & transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Source bounding box.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## bool isValid ( ) const

Checks if the bounding box coordinates are valid (minimum coordinate along the X axis is less or equal to the maximum coordinate along the X axis).
### Return value

**true** if the bounding box minimum and maximum coordinates are valid, otherwise, **false**.
## Math:: Vec3 getCenter ( ) const

Returns the center point of the current bounding box.
### Return value

Center point.
## Math:: Vec3 getSize ( ) const

Returns the size of the bounding box along the axes.
### Return value

Vector containing sizes of the bounding box along the axes, in units.
## void getPoints ( Math:: Vec3 * points , int num_points ) const

Puts the vertices of the current bounding box into the given vector.
### Arguments

- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Target vector.
- *int* **num_points** - Number of points, must be equal to 8.

## void getPlanes ( Math:: Vec4 * planes , int num_planes ) const

Puts the planes created based on the vertices of the current bounding box into the given vector.
### Arguments

- *Math::[Vec4](../../../../api/library/math/class.vec4_cpp.md) ** **planes** - Target vector.
- *int* **num_planes** - Number of planes, must be equal to 6.

## void setTransform ( const Math:: Mat4 & transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const WorldBoundSphere & bs , const Math:: Mat4 & transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## int compare ( const WorldBoundBox & bb ) const

Compares the current bounding box with the given one.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box to compare with.

### Return value

**1** if the size and position of both bounding boxes are equal; otherwise, **0**.
## int operator== ( const WorldBoundBox& bb ) const

Compares the current bounding box with the given one.
### Arguments

- *const WorldBoundBox&* **bb** - The bounding box to compare with.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## int operator!= ( const WorldBoundBox & bb ) const

Bounding boxes not equal comparison operator.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box to compare with.

### Return value

**true** if the size and position of both bounding boxes are not equal; otherwise, **false**.
## void expand ( const Math:: Vec3 & point )

Expands the current bounding box to include the given point.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

## void expand ( const Math:: Vec3 * points , int num_points )

Expands the current bounding box to enclose all given points.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - List of points to be enclosed by the bounding box.
- *int* **num_points** - Number of points to be enclosed by the bounding box.

## void expand ( const WorldBoundSphere & bs )

Expands the current bounding box to include the given bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## void expand ( const WorldBoundBox & bb )

Expands the current bounding box to include the given bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

## int inside ( const Math:: Vec3 & point ) const

Checks if the specified point is inside the current bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

### Return value

**1** if the point is inside the bounding box; otherwise, **0**.
## int inside ( const Math:: Vec3 & point , Math::Scalar radius ) const

Checks if the specified sphere is inside the current bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the center of the sphere.
- *Math::Scalar* **radius** - The sphere radius.

### Return value

**1** if the sphere is inside the bounding box; otherwise, **0**.
## int inside ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const

Checks if the given box is inside the current bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - Minimum coordinates of the box.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - Maximum coordinates of the box.

### Return value

**1** if the box is inside the bounding box; otherwise, **0**.
## int inside ( const WorldBoundSphere & bs ) const

Checks if the specified bounding sphere is inside the current bounding box.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the bounding sphere is inside the bounding box; otherwise, **0**.
## int inside ( const WorldBoundBox & bb ) const

Checks if the given bounding box is inside the current bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the bounding box is inside the bounding box; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & point ) const


Checks if the given point is inside the current bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**1** if the given point is inside the bounding box; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & point , Math::Scalar radius ) const


Checks if the given sphere is inside the current bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Cente of the sphere.
- *Math::Scalar* **radius** - Radius of the sphere.

### Return value

**1** if the sphere is inside the bounding box; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const


Checks if the box is inside the bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinates.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinates.

### Return value

**1** if the box is inside the bounding box; otherwise, **0**.
## bool insideValid ( const Math:: Vec3 * points , int num_points ) const


Checks if any of the given points is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Array of points to be checked.
- *int* **num_points** - Number of points to be checked.

### Return value

**true** if any of the given points is inside the bounding box; otherwise, **false**.
## int insideValid ( const WorldBoundSphere & bs ) const


Checks if the bounding sphere is inside the bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the bounding sphere is inside the bounding box; otherwise, **0**.
## int insideValid ( const WorldBoundBox & bb ) const


Checks if the given bounding box is inside the current bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the bounding box is inside the current bounding box; otherwise, **0**.
## int insideAll ( const WorldBoundSphere & bs ) const

Checks if the whole given bounding sphere is inside the current bounding box.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the whole sphere is inside the bounding box; otherwise, **0**.
## int insideAll ( const WorldBoundBox & bb ) const

Checks if the whole given bounding box is inside the current bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the whole box is inside the bounding box; otherwise, **0**.
## int insideAllValid ( const WorldBoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**1** if the whole bounding sphere is inside the bounding box; otherwise, **0**.
## int insideAllValid ( const WorldBoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding box.


> **Notice:** The method doesn't check if the bounding box is valid (has a positive radius).


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**1** if the whole given bounding box is inside the bounding box; otherwise, **0**.
## bool insideAllValid ( const Math::Vec3* points , int num_points ) const


Checks if all specified points are inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *const  Math::Vec3** **points** - Array of points to be checked.
- *int* **num_points** - Number of points to be checked.

### Return value

**true** if the all specified points are inside the bounding box; otherwise, **false**.
## int insideCube ( int face , const Math:: Vec3 & offset ) const

Checks if a face of the current bounding box is inside the cube represented by minimum and maximum coordinates of the bounding box.
### Arguments

- *int* **face** - The face index from **0** to **5**.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **offset** - Offset.

### Return value

**1** if the face is inside the bounding cube; otherwise, **0**.
## int rayIntersection ( const Math:: Vec3 & p , const Math:: Vec3 & direction ) const

Checks for an intersection between a ray and the current bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p** - Starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction vector of the ray.

### Return value

**1** if the given ray intersects the bounding box; otherwise, **0**.
## int irayIntersection ( const Math:: Vec3 & p , const Math:: Vec3 & idirection ) const

Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p** - Starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **idirection** - Inverse direction of the ray.

### Return value

**1** if the given ray intersects the bounding box; otherwise, **0**.
## int getIntersection ( const Math:: Vec3 & p0 , const Math:: vec3 & p1 ) const

Checks for an intersection between a line and the current bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Ending point of the line.

### Return value

**1** if the given line intersects the bounding box; otherwise, **0**.
## int rayIntersectionValid ( const Math:: Vec3 & point , const Math:: Vec3 & direction ) const


Checks for an intersection between a ray and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - Direction vector of the ray.

### Return value

**1** if the given ray intersects the bounding box; otherwise, **0**.
## int irayIntersectionValid ( const Math:: Vec3 & p , const Math:: Vec3 & idirection ) const

Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p** - Starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **idirection** - Inverse direction of the ray.

### Return value

**1** if the given ray intersects the bounding box; otherwise, **0**.
## int getIntersectionValid ( const Math:: Vec3 & p0 , const Math:: vec3 & p1 ) const


Checks for an intersection between a line and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Enging point of the line.

### Return value

**1** if the given line intersects the bounding box; otherwise, **0**.
## double distance ( ) const

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance in units, if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../api/library/math/constants_cpp.md)**.
## double distance ( const Math:: Vec3 & point ) const

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of a point.

### Return value

Distance, in units.
## double distanceValid ( ) const

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance from the given point to the closest vertex of the bounding box, in units.
## double distanceValid ( const Math:: Vec3 & point ) const

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

### Return value

Distance from the given point to the closest vertex of the bounding box, in units.
## WorldBoundBox operator* ( const dmat4 & m , const WorldBoundBox & bs )

Returns the bounding box with the specified transformation matrix applied.
### Arguments

- *const [dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **m** - Transform matrix.
- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bs** - The bounding sphere.

### Return value

The bounding sphere with the specified transform.
