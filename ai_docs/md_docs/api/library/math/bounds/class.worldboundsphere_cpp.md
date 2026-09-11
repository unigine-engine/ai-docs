# Unigine::WorldBoundSphere Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding sphere in double precision coordinates.


By using this structure you can easily find the common bounding sphere for several objects by expanding the bounding sphere.


## WorldBoundSphere Class

### Members

---

## static WorldBoundSpherePtr create ( )

Constructor. Creates an empty bounding sphere.
## WorldBoundSphere ( double x , double y , double z , double radius )

Constructor. Initialization by the coordinates of the center and radius of the bounding sphere.
### Arguments

- *double* **x** - X-coordinate of the center of the bounding sphere.
- *double* **y** - Y-coordinate of the center of the bounding sphere.
- *double* **z** - Z-coordinate of the center of the bounding sphere.
- *double* **radius** - Radius of the bounding sphere.

## WorldBoundSphere ( Math:: Vec3 & center , Math::Scalar radius )

Constructor. Initializes bounding sphere by the center and radius of the bounding sphere.
### Arguments

- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **center** - The bounding sphere center.
- *Math::Scalar* **radius** - The bounding sphere radius.

## WorldBoundSphere ( const dvec3 * points , int num_points , bool optimal )

Constructor. Initialization by the vector of points.
### Arguments

- *const [dvec3](../../../../api/library/math/class.dvec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points in the vector.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If false, the sphere will be expanded to include all given points.

## WorldBoundSphere ( const WorldBoundSphere & bs )

Constructor. Initializes by given bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## WorldBoundSphere ( const WorldBoundSphere & bs , const Math:: Mat4 & transform )

Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## WorldBoundSphere ( const BoundSphere & bs )

Constructor. Initializes by given bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

## WorldBoundSphere ( const BoundSphere & bs , const Math:: Mat4 & transform )

Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## WorldBoundSphere ( const WorldBoundBox & bb )

Constructor. Initializes by given bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

## WorldBoundSphere & operator= ( const WorldBoundSphere & bs )

Assignment operator for the bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## void clear ( )

Clears the bounding sphere.
## void setCenter ( const dvec3 & center )

Sets the specified coordinates for the center of the bounding sphere.
### Arguments

- *const [dvec3](../../../../api/library/math/class.dvec3_cpp.md) &* **center** - Coordinates of the center of the bounding sphere.

## void set ( const Math:: Vec3 & center , Math::Scalar radius )

Sets the bounding sphere by its center and radius.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **center** - The bounding sphere center.
- *Math::Scalar* **radius** - The bounding sphere radius.

## void set ( double x_ , double y_ , double z_ , double radius_ )

Sets the bounding sphere by the specified coordinates of the center and radius.
### Arguments

- *double* **x_** - X-coordinate of the center of the bounding sphere.
- *double* **y_** - Y-coordinate of the center of the bounding sphere.
- *double* **z_** - Z-coordinate of the center of the bounding sphere.
- *double* **radius_** - Radius of the bounding sphere.

## void set ( const Math:: Vec3 * points , int num_points , bool optimal )

Set the bounding sphere by a vector of points.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points in the vector.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If **false**, the sphere will be expanded for including all the given points.

## void set ( const WorldBoundSphere & bs )

Sets the bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## void set ( const WorldBoundSphere & bs , const Math:: Mat4 & transform )

Sets the bounding sphere by a bounding sphere with a transformation matrix taken into account.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void set ( const BoundSphere & bs )

Sets the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

## void set ( const BoundSphere & bs , const Math:: Mat4 & transform )

Sets the bounding sphere by a bounding sphere with a transformation matrix taken into account.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void set ( const WorldBoundBox & bb )

Sets the bounding sphere by the bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

## bool isValid ( ) const

Checks the bounding sphere status.
### Return value

**true** if the bounding sphere radius has a positive value.
## void setTransform ( const Math:: Mat4 & transform )

Sets the given transformation matrix for the bounding sphere.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## int compare ( const WorldBoundSphere & bs )

Compares the bounding sphere with the given one. The degree of precision is equal to **1.0e-6f**.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are equal; otherwise, **0**.
## int operator== ( const WorldBoundSphere & bs ) const

Compares the bounding sphere with the given one according to the degree of precision equal to **1.0e-6f**.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are equal; otherwise, **0**.
## int operator!= ( const WorldBoundSphere & bs ) const

Bounding spheres not equal comparison operator.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are not equal; otherwise, **0**.
## void expand ( const Math:: Vec3 & point )

Expands the current bounding sphere for including given point.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.

## void expand ( const Math:: Vec3 * points , int num_points )

Expands the current bounding sphere for including all points in the vector.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## void expand ( const WorldBoundSphere & bs )

Expands the current bounding sphere for including given bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

## void expand ( const WorldBoundBox & bb )

Expands the current bounding sphere for including given bounding box.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

## void expandRadius ( const Math:: Vec3 & point )

Expands the radius of the bounding sphere.
Expands the radius of the bounding sphere.


```cpp
float r = length(center - point);
if (center.w < r)
	radius = r;

```


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates setting the end point of radius.

## void expandRadius ( const Math:: Vec3 * points , int num_points )

Expands the radius of the current bounding sphere for including all points in the vector.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## void expandRadius ( const WorldBoundSphere & bs )


Expands the radius of the bounding sphere by using the radius of the given bounding sphere.


```cpp
double r = length(bs.center - center) + bs.radius;
if (radius < r)
	radius = r;

```


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.

## void expandRadius ( const BoundBox & bb )

Expands the radius of the bounding sphere by using the max and min points of the given bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## int inside ( const Math:: Vec3 & point ) const

Checks if the given point is inside the current bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.

### Return value

**1** if the given point is inside the bounding sphere; otherwise, **0**.
## int inside ( const Math:: Vec3 & point , Math::Scalar radius ) const

Checks if the sphere is inside the bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the center of the sphere .
- *Math::Scalar* **radius** - The sphere radius.

### Return value

**1** if the sphere is inside the bounding sphere; otherwise, **0**.
## int inside ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const

Checks if the box is inside the bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinates.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinates.

### Return value

**1** if the box is inside the bounding sphere; otherwise, **0**.
## int inside ( const WorldBoundSphere & bs ) const

Checks if the specified bounding sphere is inside the current bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the specified bounding sphere is inside the current bounding sphere; otherwise, **0**.
## int inside ( const WorldBoundBox & bb ) const

Checks if the bounding box is inside the bounding sphere.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the bounding box is inside the bounding sphere; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & point ) const


Checks if the given point is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**1** if the given point is inside the bounding sphere; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & point , Math::Scalar radius ) const


Checks if the given sphere is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Cente of the sphere.
- *Math::Scalar* **radius** - Radius of the sphere.

### Return value

**1** if the sphere is inside the bounding sphere; otherwise, **0**.
## int insideValid ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const


Checks if the box is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinates.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinates.

### Return value

**1** if the box is inside the bounding sphere; otherwise, **0**.
## int insideValid ( const WorldBoundSphere & bs ) const


Checks if the bounding sphere is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the bounding sphere is inside the bounding sphere; otherwise, **0**.
## int insideValid ( const WorldBoundBox & bb ) const


Checks if the bounding box is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the bounding box is inside the bounding sphere; otherwise, **0**.
## int insideAll ( const WorldBoundSphere & bs ) const

Checks if the whole specified bounding sphere is inside the current bounding sphere.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the whole specified sphere is inside the current bounding sphere; otherwise, **0**.
## int insideAll ( const WorldBoundBox & bb ) const

Checks if the whole bounding box is inside the bounding sphere.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the whole box is inside the bounding sphere; otherwise, **0**.
## int insideAllValid ( const WorldBoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**1** if the whole bounding sphere is inside the bounding sphere; otherwise, **0**.
## int insideAllValid ( const WorldBoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**1** if the whole bounding box is inside the bounding sphere; otherwise, **0**.
## bool rayIntersection ( const Math:: Vec3 & point , const Math:: Vec3 & direction ) const

Checks for an intersection of a ray with the current bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector of the ray.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 ) const

Checks for an intersection of a line with the current bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point of the line.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool rayIntersectionValid ( const Math:: Vec3 & point , const Math:: Vec3 & direction ) const


Checks for an intersection of a ray with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The starting point of the ray.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector of the ray.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool getIntersectionValid ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 ) const


Checks for an intersection of a line with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point of the line.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## Math::Scalar distance ( ) const

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## Math::Scalar distance ( const Math:: Vec3 & point ) const

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

### Return value

Distance from the point, in units.
## Math::Scalar distanceValid ( ) const

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## Math::Scalar distanceValid ( const Math:: Vec3 & point ) const

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point

### Return value

Distance from the point, in units.
## bool isCameraVisible ( const Math:: Vec3 & camera , Math::Scalar min_distance , Math::Scalar max_distance ) const

Returns a value indicating if the bounding sphere is within the camera visibility distance.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **camera** - Coordinates of the camera position.
- *Math::Scalar* **min_distance** - Minimum visibility distance, in meters.
- *Math::Scalar* **max_distance** - Maximum visibility distance, in meters.

### Return value

**true** if the bounding sphere is within the camera visibility distance; otherwise, **false**.
## WorldBoundSphere operator* ( const dmat4 & m , const WorldBoundSphere & bs )

Returns the bounding sphere with the specified transformation matrix applied.
### Arguments

- *const [dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **m** - Transform matrix.
- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

The bounding sphere with the specified transform.
