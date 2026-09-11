# Unigine.WorldBoundSphere Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding sphere in double precision coordinates.


By using this structure you can easily find the common bounding sphere for several objects by expanding the bounding sphere.


## WorldBoundSphere Class

### Members

---

## WorldBoundSphere ( dvec3 center , double radius )

Constructor. Initialization by the center and radius of the bounding sphere.
### Arguments

- *dvec3* **center** - The bounding sphere center.
- *double* **radius** - The bounding sphere radius.

## WorldBoundSphere ( dvec3[] points , bool optimal )

Constructor. Initialization by the array of points.
### Arguments

- *dvec3[]* **points** - Array of points.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If false, the sphere will be expanded to include all given points.

## WorldBoundSphere ( WorldBoundSphere bs )

Constructor. Initialization by the bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - The bounding sphere.

## WorldBoundSphere ( WorldBoundSphere bs , mat4 transform )

Constructor. Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - The bounding sphere.
- *mat4* **transform** - Transformation matrix.

## WorldBoundSphere ( WorldBoundSphere bs , dmat4 transform )

Constructor. Initialization by the bounding sphere and setting the given transformation matrix to the new bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - The bounding sphere.
- *dmat4* **transform** - Transformation matrix.

## WorldBoundSphere ( WorldBoundBox bb )

Constructor. Initialization by the bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - The bounding box.

## WorldBoundSphere ( BoundSphere bs )

Constructor. Initialization by the single-precision bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - The bounding sphere.

## void Set ( BoundSphere bs )

Sets the value using the specified argument.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## WorldBoundSphere operator* ( dmat4 m , WorldBoundSphere bs )

Multiplies the matrix by the bounding sphere and returns the resulting bounding sphere.
### Arguments

- *dmat4* **m** - Matrix.
- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

Resulting bounding sphere.
## void Set ( dvec3 center , double radius )

Sets the bounding sphere using the specified argument(s).
### Arguments

- *dvec3* **center** - The bounding sphere center.
- *double* **radius** - The bounding sphere radius.

## void Set ( dvec3[] points , bool optimal )

Sets the bounding sphere using the specified arguments.
### Arguments

- *dvec3[]* **points** - Array of points.
- *bool* **optimal** - Flag defining if the optimal sphere should be used. If **false**, the sphere will be expanded for including all the given points.

## void Set ( WorldBoundSphere bs )

Sets the bounding sphere using the specified arguments.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

## void Set ( WorldBoundSphere bs , dmat4 transform )

Sets the bounding sphere using the specified arguments.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Set ( WorldBoundBox bb )

Sets the bounding sphere by the bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

## void Clear ( )

Clears the bounding sphere by setting all components/elements to 0.
## bool Equals ( WorldBoundSphere other )

Checks if the bounding sphere and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **other** - Bounding sphere to be checked for equality.

### Return value

**true** if the radii and the centers of both bounding spheres are equal; otherwise, **false**.
## bool EqualsNearly ( WorldBoundSphere other , double epsilon )

Checks if the bounding sphere and the specified argument represent the same value with regard to the specified accuracy (epsilon).
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **other** - Bounding sphere to be checked for equality.
- *double* **epsilon** - Epsilon value, that determines accuracy of comparison.

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
## void SetTransform ( dmat4 transform )

Sets the given transformation matrix to bounding sphere.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Expand ( dvec3 point )

Expands the current bounding sphere to include the given point.
### Arguments

- *dvec3* **point** - Coordinates of the point.

## void Expand ( dvec3[] points )

Expands the current bounding sphere for including all points in the array.
### Arguments

- *dvec3[]* **points** - Array of points.

## void Expand ( BoundSphere bs )

Expands the current bounding sphere to include the given bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere to be included.

## void Expand ( WorldBoundBox bb )

Expands the current bounding sphere to include the given bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box to be included.

## void ExpandRadius ( dvec3 point )

Expands the radius of the bounding sphere.
### Arguments

- *dvec3* **point** - Point coordinates setting the end point of radius.

## void ExpandRadius ( dvec3[] points )

Expands the radius of the current bounding sphere for including all points of the array.
### Arguments

- *dvec3[]* **points** - Array of points.

## void ExpandRadius ( WorldBoundSphere bs )

Expands the radius of the bounding sphere by using the radius of the given bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

## void ExpandRadius ( WorldBoundBox bb )

Expands the radius of the bounding sphere by using the max and min points of the given bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

## bool Inside ( dvec3 point )

Checks if the given point is inside the current bounding sphere.
### Arguments

- *dvec3* **point** - Point coordinates.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool Inside ( dvec3 point , double radius )

Checks if the sphere defined by the arguments is inside the bounding sphere.
### Arguments

- *dvec3* **point** - Center of the sphere.
- *double* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool Inside ( dvec3 min , dvec3 max )

Checks if the box specified by the arguments is inside the bounding sphere.
### Arguments

- *dvec3* **min** - Minimum coordinates of the box (lower limit).
- *dvec3* **max** - Maximum coordinates of the box (upper limit).

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( dvec3 point )

Checks if the given point is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *dvec3* **point** - Point coordinates.

### Return value

**true** if the given point is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( dvec3 point , double radius )

Checks if the sphere specified in the argument is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *dvec3* **point** - Cente of the sphere.
- *double* **radius** - Radius of the sphere.

### Return value

**true** if the sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( dvec3 min , dvec3 max )

Checks if the box specified in the argument is inside the current bounding sphere.

> **Notice:** The method doesn't check if the current bounding sphere is valid.

### Arguments

- *dvec3* **min** - Minimum coordinates of the box (lower limit).
- *dvec3* **max** - Maximum coordinates of the box (upper limit).

### Return value

**true** if the box is inside the bounding sphere; otherwise, **false**.
## bool Inside ( WorldBoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool Inside ( WorldBoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding sphere.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( WorldBoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideValid ( WorldBoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideAll ( WorldBoundSphere bs )

Checks if the whole specified bounding sphere is inside the current bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideAll ( WorldBoundBox bb )

Checks if the whole specified bounding box is inside the current bounding sphere.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool InsideAllValid ( WorldBoundSphere bs )

Checks if the whole bounding sphere specified in the argument is completely inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding sphere; otherwise, **false**.
## bool InsideAllValid ( WorldBoundBox bb )

Checks if the whole bounding box specified in the argument is completely inside the current bounding sphere.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding sphere; otherwise, **false**.
## bool RayIntersection ( dvec3 point , dvec3 direction )

Checks for an intersection between a ray and the current bound.
### Arguments

- *dvec3* **point** - The starting point of the ray.
- *dvec3* **direction** - Direction vector coordinates.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool GetIntersection ( dvec3 p0 , dvec3 p1 )

Checks for an intersection of a line with the current bounding sphere.
### Arguments

- *dvec3* **p0** - The starting point of the line.
- *dvec3* **p1** - The ending point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool RayIntersectionValid ( dvec3 point , dvec3 direction )

Checks for an intersection between a ray and the current bound.

> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).

### Arguments

- *dvec3* **point** - The starting point of the ray.
- *dvec3* **direction** - Direction vector coordinates.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## bool GetIntersectionValid ( dvec3 p0 , dvec3 p1 )


Checks for an intersection of a line with the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *dvec3* **p0** - The starting point of the line.
- *dvec3* **p1** - The starting point of the line.

### Return value

**true** if an intersection has occurred; otherwise, **false**.
## double Distance ( )

Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.
### Return value

Distance from the origin, in units.
## double Distance ( dvec3 point )

Returns the distance from the given point to the closest point of the current bounding sphere.
### Arguments

- *dvec3* **point** - Coordinates of the point.

### Return value

Distance from the point, in units.
## double DistanceValid ( )


Returns the distance from the origin of coordinates to the closest point of the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Return value

Distance from the origin, in units.
## double DistanceValid ( dvec3 point )


Returns the distance from the given point to the closest point of the current bounding sphere.


> **Notice:** This method doesn't check if the current bounding sphere is valid (has a positive radius).


### Arguments

- *dvec3* **point** - Coordinates of the point.

### Return value

Distance from the origin, in units.
## bool IsCameraVisible ( dvec3 camera , double min_distance , double max_distance )

Returns a value indicating if the bounding sphere is within the camera visibility distance.
### Arguments

- *dvec3* **camera** - Camera position.
- *double* **min_distance** - Minimum visibility distance, in units.
- *double* **max_distance** - Maximum visibility distance, in units.

### Return value

**true** if the bounding sphere is within the camera visibility distance; otherwise, **false**.
