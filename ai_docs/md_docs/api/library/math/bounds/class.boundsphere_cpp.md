# Unigine::BoundSphere Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding sphere in single precision coordinates.


> **Notice:** Instances of this structure are deleted automatically when it is necessary.


In case of double precision coordinates, the bounding sphere should be constructed by using the **[WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md)** structure.  It includes the same functions as the *BoundSphere* structure, but its functions deal with the double precision coordinates.


> **Notice:** To support both single and double precision builds, you can use the *WorldBoundSphere* structure only. The engine will automatically substitute it with the *BoundSphere* if it is required.


## BoundSphere Class

### Members

---

## BoundSphere ( )

Constructor. Creates an empty bounding sphere.
## BoundSphere ( const vec3 & center , float radius )

Constructor. Initialization by the center and radius of the bounding sphere.
### Arguments

- *const [vec3](../../../../api/library/math/class.vec3_cpp.md) &* **center** - The bounding sphere center.
- *float* **radius** - The bounding sphere radius.

## BoundSphere ( float x , float y , float z , float radius )

Constructor. Initialization by the coordinates of the center and radius of the bounding sphere.
### Arguments

- *float* **x** - X-coordinate of the center of the bounding sphere.
- *float* **y** - Y-coordinate of the center of the bounding sphere.
- *float* **z** - Z-coordinate of the center of the bounding sphere.
- *float* **radius** - Radius of the bounding sphere.

## BoundSphere ( const vec3 * points , int num_points , bool optimal )

Constructor. Initialization by the vector of points.
### Arguments

- *const [vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points in the vector.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If false, the sphere will be expanded to include all given points.

## BoundSphere ( const BoundSphere & bs )

Initialization by the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

## BoundSphere ( const BoundSphere & bs , const mat4 & transform )

Constructor. Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const [mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## explicit BoundSphere ( const BoundBox & bb )

Constructor. Initialization by the bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

## BoundSphere & operator= ( const BoundSphere & bs )

Assignment operator for the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

## void clear ( )

Clears the bounding sphere.
## void set ( const Math:: vec3 & center , float radius )

Sets the bounding sphere by its center and radius.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **center** - Center of the bounding sphere.
- *float* **radius** - Radius of the bounding sphere.

## void set ( float x_ , float y_ , float z_ , float radius_ )

Sets the bounding sphere by the specified coordinates of the center and radius.
### Arguments

- *float* **x_** - X-coordinate of the center of the bounding sphere.
- *float* **y_** - Y-coordinate of the center of the bounding sphere.
- *float* **z_** - Z-coordinate of the center of the bounding sphere.
- *float* **radius_** - Radius of the bounding sphere.

## void set ( const Math:: vec3 * points , int num_points , bool optimal )

Set the bounding sphere by a vector of points.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points in the vector.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If **false**, the sphere will be expanded for including all the given points.

## void set ( const BoundSphere & bs )

Sets the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

## void set ( const BoundSphere & bs , const Math:: mat4 & transform )

Sets the bounding sphere by a bounding sphere with a transformation matrix taken into account.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void set ( const BoundBox & bb )

Sets the bounding sphere by the bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## void setCenter ( const vec3& center )

Sets the specified coordinates for the center of the bounding sphere.
### Arguments

- *const vec3&* **center** - Coordinates of the center of the bounding sphere.

## void setTransform ( const Math:: mat4 & transform )

Sets the given transformation matrix to bounding sphere.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setTransform ( const Math:: dmat4 & transform )

Sets the given transformation matrix to bounding sphere.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **transform** - Transformation matrix.

## int compare ( const BoundSphere & bs )

Compares the bounding sphere with the given one. The degree of precision is equal to **1.0e-6f**.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are equal; otherwise, **0**.
## int operator== ( const BoundSphere & bs ) const

Compares the bounding sphere with the given one according to the degree of precision equal to **1.0e-6f**.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are equal; otherwise, **0**.
## int operator!= ( const BoundSphere & bs ) const

Bounding spheres not equal comparison operator.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere to compare with.

### Return value

**1** if the radii and the centers of both bounding spheres are not equal; otherwise, **0**.
## BoundSphere operator* ( const mat4 & m , const BoundSphere & bs )

Returns the bounding sphere with the specified transformation matrix applied.
### Arguments

- *const [mat4](../../../../api/library/math/class.mat4_cpp.md) &* **m** - Transform matrix.
- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

The bounding sphere with the specified transform.
## BoundSphere operator* ( const dmat4 & m , const BoundSphere & bs )

Returns the bounding sphere with the specified transformation matrix applied.
### Arguments

- *const [dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **m** - Transform matrix.
- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

The bounding sphere with the specified transform.
## void expand ( const Math:: vec3 & point )

Expands the current bounding sphere to include the given point.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

## void expand ( const Math:: vec3 * points , int num_points )

Expands the current bounding sphere for including all points in the vector.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## void expand ( const BoundSphere & bs )

Expands the current bounding sphere to include the given bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere to be included.

## void expand ( const BoundBox & bb )

Expands the current bounding sphere to include the given bounding box.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box to be included.

## void expandRadius ( const Math:: vec3 & point )

Expands the radius of the bounding sphere.
Expands the radius of the bounding sphere.


```cpp
float r = length(center - point);
if (center.w < r)
	radius = r;

```


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates setting the end point of radius.

## void expandRadius ( const Math:: vec3 * points , int num_points )

Expands the radius of the current bounding sphere for including all points in the vector.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

## void expandRadius ( const BoundSphere & bs )


Expands the radius of the bounding sphere by using the radius of the given bounding sphere.


```cpp
float r = length(bs.center - center) + bs.radius;
if (radius < r)
	radius = r;

```


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

## void expandRadius ( const BoundBox & bb )


Expands the radius of the bounding sphere by using the max and min points of the given bounding box. It uses the [expandRadius](#expandRadius_const_vec3_ref_void) method.


```cpp
const vec3 &min = bb.getMin();
const vec3 &max = bb.getMax();
expandRadius(vec3(min.x, min.y, min.z));
expandRadius(vec3(max.x, min.y, min.z));
expandRadius(vec3(min.x, max.y, min.z));
expandRadius(vec3(max.x, max.y, min.z));
expandRadius(vec3(min.x, min.y, max.z));
expandRadius(vec3(max.x, min.y, max.z));
expandRadius(vec3(min.x, max.y, max.z));
expandRadius(vec3(max.x, max.y, max.z));

```


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

## bool inside ( const Math:: vec3 & point ) const

Checks if the given point is inside the current bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool inside ( const Math:: vec3 & point , float radius ) const

Checks if the sphere is inside the bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Center of the sphere.
- *float* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool inside ( const Math:: vec3 & min , const Math:: vec3 & max ) const

Checks if the box is inside the bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinates.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinates.

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool inside ( const BoundSphere & bs ) const

Checks if the specified bounding sphere is inside the bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the specified bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool inside ( const BoundBox & bb ) const

Checks if the bounding box is inside the bounding sphere.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & point ) const


Checks if the given point is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & point , float radius ) const


Checks if the given sphere is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Cente of the sphere.
- *float* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool insideValid ( const Math:: vec3 & min , const Math:: vec3 & max ) const


Checks if the box is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinates.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinates.

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool insideValid ( const BoundSphere & bs ) const


Checks if the bounding sphere is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool insideValid ( const BoundBox & bb ) const


Checks if the bounding box is inside the bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool insideAll ( const BoundSphere & bs ) const

Checks if the whole specified bounding sphere is inside the current bounding sphere.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool insideAll ( const BoundBox & bb ) const

Checks if the whole specified bounding box is inside the current bounding sphere.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool insideAllValid ( const BoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool insideAllValid ( const BoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding sphere.


> **Notice:** The method doesn't check if the bounding sphere is valid (has a positive radius).


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool rayIntersection ( const Math:: vec3 & point , const Math:: vec3 & direction ) const

Checks for an intersection of a ray with the current bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector of the ray.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool getIntersection ( const Math:: vec3 & p0 , const Math:: vec3 & p1 ) const

Checks for an intersection of a line with the current bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool rayIntersectionValid ( const Math:: vec3 & point , const Math:: vec3 & direction ) const


Checks for an intersection of a ray with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The starting point of the ray.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector of the ray.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool getIntersectionValid ( const Math:: vec3 & p0 , const Math:: vec3 & p1 ) const


Checks for an intersection of a line with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point of the line.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## float distance ( ) const

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## float distance ( const Math:: vec3 & point ) const

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the point.

### Return value

Distance from the point, in units.
## float distanceValid ( ) const

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## float distanceValid ( const Math:: vec3 & point ) const

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point

### Return value

Distance from the point, in units.
## bool isValid ( ) const

Checks the bounding sphere status.
### Return value

**true** if the bounding sphere radius has a positive value; otherwise, **false**.
## bool isCameraVisible ( const vec3& camera , float min_distance , float max_distance ) const

Returns a value indicating if the bounding sphere is within the camera visibility distance.
### Arguments

- *const vec3&* **camera** - Coordinates of the camera position.
- *float* **min_distance** - Minimum visibility distance, in meters.
- *float* **max_distance** - Maximum visibility distance, in meters.

### Return value

**true** if the bounding sphere is within the camera visibility distance; otherwise, **false**.
