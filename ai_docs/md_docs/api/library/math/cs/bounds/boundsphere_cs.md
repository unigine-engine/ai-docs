# Unigine.BoundSphere Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding sphere in single precision coordinates.


Instances of this structure are deleted automatically, when necessary.


In case of double precision coordinates, the bounding sphere should be constructed by using the **[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)** structure. It includes the same functions as the *BoundSphere* structure, but its functions deal with the double precision coordinates.


To support both single and double precision builds, you can use the *WorldBoundSphere* structure only. The engine will automatically substitute it with the *BoundSphere*, if required.


## BoundSphere Class

### Members

---

## BoundSphere ( vec3 center , float radius )

Constructor. Initialization by the center and radius of the bounding sphere.
### Arguments

- *vec3* **center** - The bounding sphere center.
- *float* **radius** - The bounding sphere radius.

## BoundSphere ( vec3[] points , bool optimal )

Constructor. Initialization by the array of points.
### Arguments

- *vec3[]* **points** - Array of points.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If false, the sphere will be expanded to include all given points.

## BoundSphere ( BoundSphere bs )

Constructor. Initialization by the bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - The bounding sphere.

## BoundSphere ( BoundSphere bs , mat4 transform )

Constructor. Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - The bounding sphere.
- *mat4* **transform** - Transformation matrix.

## BoundSphere ( BoundSphere bs , dmat4 transform )

Constructor. Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - The bounding sphere.
- *dmat4* **transform** - Transformation matrix.

## BoundSphere ( BoundBox bb )

Constructor. Initialization by the bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - The bounding box.

## BoundSphere operator* ( mat4 m , BoundSphere bs )

Multiplies the matrix by the bounding sphere and returns the resulting bounding sphere.
### Arguments

- *mat4* **m** - Matrix.
- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

Resulting bounding sphere.
## BoundSphere operator* ( dmat4 m , BoundSphere bs )

Multiplies the matrix by the bounding sphere and returns the resulting bounding sphere.
### Arguments

- *dmat4* **m** - Matrix.
- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

Resulting bounding sphere.
## void Set ( vec3 center , float radius )

Sets the bounding sphere using the specified arguments.
### Arguments

- *vec3* **center** - The bounding sphere center.
- *float* **radius** - The bounding sphere radius.

## void Set ( vec3[] points , bool optimal )

Sets the bounding sphere using the specified arguments.
### Arguments

- *vec3[]* **points** - Array of points.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If **false**, the sphere will be expanded for including all the given points.

## void Set ( BoundSphere bs )

Sets the bounding sphere using the specified arguments.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## void Set ( BoundSphere bs , mat4 transform )

Sets the bounding sphere using the specified arguments.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.
- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void Set ( BoundSphere bs , dmat4 transform )

Sets the bounding sphere using the specified arguments.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Set ( BoundBox bb )

Sets the bounding sphere by the bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## void Clear ( )

Clears the bounding sphere by setting all components/elements to 0.
## bool Equals ( BoundSphere other )

Checks if the bounding sphere and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **other** - Bounding sphere to be checked for equality.

### Return value

**true** if the radii and the centers of both bounding spheres are equal; otherwise, **false**.
## bool EqualsNearly ( BoundSphere other , float epsilon )

Checks if the bounding sphere and the specified argument represent the same value with regard to the specified accuracy (epsilon).
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **other** - Bounding sphere to be checked for equality.
- *float* **epsilon** - Epsilon value, that determines accuracy of comparison.

### Return value

**true** if the radii and the centers of both bounding spheres are equal; otherwise, **false**.
## bool Equals ( object obj )

Checks if the bounding sphere and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[object](../../../../../api/library/objects/class.object_cs.md)* **obj** - Object to be checked for equality.

### Return value

**true** if the object and the bounding sphere are equal; otherwise, **false**.
## int GetHashCode ( )

Returns a hash code for the current object. Serves as the default hash function.
### Return value

Hash code.
## void SetTransform ( mat4 transform )

Sets the given transformation matrix to bounding sphere.
### Arguments

- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void SetTransform ( dmat4 transform )

Sets the given transformation matrix to bounding sphere.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Expand ( vec3 point )

Expands the current bounding sphere to include the given point.
### Arguments

- *vec3* **point** - Coordinates of the point.

## void Expand ( vec3[] points )

Expands the current bounding sphere for including all points in the array.
### Arguments

- *vec3[]* **points** - Array of points.

## void Expand ( BoundSphere bs )

Expands the current bounding sphere to include the given bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere to be included.

## void Expand ( BoundBox bb )

Expands the current bounding sphere to include the given bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box to be included.

## void ExpandRadius ( vec3 point )

Expands the radius of the bounding sphere.
### Arguments

- *vec3* **point** - Point coordinates setting the end point of radius.

## void ExpandRadius ( vec3[] points )

Expands the radius of the current bounding sphere for including all points of the array.
### Arguments

- *vec3[]* **points** - Array of points.

## void ExpandRadius ( BoundSphere bs )

Expands the radius of the bounding sphere by using the radius of the given bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## void ExpandRadius ( BoundBox bb )

Expands the radius of the bounding sphere by using the max and min points of the given bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## bool Inside ( vec3 point )

Checks if the given point is inside the current bounding sphere.
### Arguments

- *vec3* **point** - Point coordinates.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool Inside ( vec3 point , float radius )

Checks if the sphere defined by the arguments is inside the bounding sphere.
### Arguments

- *vec3* **point** - Center of the sphere.
- *float* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool Inside ( vec3 min , vec3 max )

Checks if the box is inside the bounding sphere.
### Arguments

- *vec3* **min** - Minimum coordinates of the box.
- *vec3* **max** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( vec3 point )

Checks if the given point is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *vec3* **point** - Point coordinates.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( vec3 point , float radius )

Checks if the sphere specified in the argument is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *vec3* **point** - Cente of the sphere.
- *float* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( vec3 min , vec3 max )

Checks if the box specified in the argument is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *vec3* **min** - Minimum coordinates of the box (lower limit).
- *vec3* **max** - Maximum coordinates of the box (upper limit).

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool Inside ( BoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool Inside ( BoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding sphere.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( BoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( BoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideAll ( BoundSphere bs )

Checks if the whole specified bounding sphere is inside the current bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideAll ( BoundBox bb )

Checks if the whole specified bounding box is inside the current bounding sphere.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideAllValid ( BoundSphere bs )

Checks if the whole bounding sphere specified in the argument is completely inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideAllValid ( BoundBox bb )

Checks if the whole bounding box specified in the argument is completely inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool RayIntersection ( vec3 point , vec3 direction )

Checks for an intersection between a ray and the current bound.
### Arguments

- *vec3* **point** - The starting point of the ray.
- *vec3* **direction** - Direction vector coordinates.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool GetIntersection ( vec3 p0 , vec3 p1 )

Checks for an intersection of a line with the current bounding sphere.
### Arguments

- *vec3* **p0** - The starting point of the line.
- *vec3* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool RayIntersectionValid ( vec3 point , vec3 direction )

Checks for an intersection between a ray and the current bound.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *vec3* **point** - The starting point of the ray.
- *vec3* **direction** - Direction vector coordinates.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool GetIntersectionValid ( vec3 p0 , vec3 p1 )


Checks for an intersection of a line with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *vec3* **p0** - The starting point of the line.
- *vec3* **p1** - The starting point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## float Distance ( )

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## float Distance ( vec3 point )

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *vec3* **point** - Coordinates of the point.

### Return value

Distance from the point, in units.
## float DistanceValid ( )


Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Return value

Distance from the origin, in units.
## float DistanceValid ( vec3 point )


Returns the distance from the given point to the closest point of the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *vec3* **point** - Coordinates of the point.

### Return value

Distance from the origin, in units.
## bool IsCameraVisible ( vec3 camera , float min_distance , float max_distance )

Returns a value indicating if the bounding sphere is within the camera visibility distance.
### Arguments

- *vec3* **camera** - Camera position.
- *float* **min_distance** - Minimum visibility distance, in units.
- *float* **max_distance** - Maximum visibility distance, in units.

### Return value

**true** if the bounding sphere is within the camera visibility distance; otherwise, **false**.
