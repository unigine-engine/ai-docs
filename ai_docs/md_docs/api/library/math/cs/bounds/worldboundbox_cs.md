# Unigine.WorldBoundBox Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding box in double precision coordinates.


Bounding boxes has better precision quality but it takes more time for calculation in comparison with bounding spheres.


By using this structure you can easily find the common bounding box for several objects by expanding the bounding box.


## WorldBoundBox Class

### Members

---

## WorldBoundBox ( dvec3 min_ , dvec3 max_ )

Constructor. Initializes the bounding box by the minimum and maximum coordinates.
### Arguments

- *dvec3* **min_** - Minimum coordinates of the bounding box.
- *dvec3* **max_** - Maximum coordinates of the bounding box.

## WorldBoundBox ( dvec3[] points )

Constructor. Initializes the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *dvec3[]* **points** - Array of points to be enclosed by the bounding box.

## WorldBoundBox ( WorldBoundBox bb )

Constructor. Initializes the bounding box equal to the bounding box specified in the argument.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

## WorldBoundBox ( WorldBoundBox bb , dmat4 transform )

Constructor. Initializes the bounding box by the given bounding box with the given transformation matrix.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.
- *dmat4* **transform** - Transformation matrix.

## WorldBoundBox ( BoundBox bb )

Constructor. Initializes the bounding box by the given bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## WorldBoundBox ( BoundBox bb , dmat4 transform )

Constructor. Initializes the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *dmat4* **transform** - Transformation matrix.

## WorldBoundBox ( WorldBoundSphere bs )

Constructor. Initializes the bounding box by the bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

## WorldBoundBox operator* ( dmat4 m , WorldBoundBox bs )

Multiplies the matrix by the bounding box and returns the resulting bounding box.
### Arguments

- *dmat4* **m** - Matrix.
- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bs** - Bounding box.

### Return value

Resulting bounding box.
## void Set ( dvec3 min_ , dvec3 max_ )

Initializes the bounding box by the minimum and maximum coordinates.
### Arguments

- *dvec3* **min_** - Minimum coordinates of the bounding box.
- *dvec3* **max_** - Maximum coordinates of the bounding box.

## void Set ( dvec3[] points )

Sets the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *dvec3[]* **points** - Array of points to be enclosed by the bounding box.

## void Set ( WorldBoundBox bb )

Sets the bounding box equal to the bounding box specified in the argument.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

## void Set ( WorldBoundBox bb , mat4 transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.
- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void Set ( WorldBoundBox bb , dmat4 transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Set ( BoundBox bb , mat4 transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void Set ( BoundBox bb , dmat4 transform )

Sets the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Set ( WorldBoundSphere bs )

Sets the bounding box by the bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

## void Clear ( )

Clears the bounding box by setting all components/elements to 0.
## bool Equals ( WorldBoundBox other )

Checks if the current bounding box is equal to the specified argument considering the predefined accuracy (epsilon).
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **other** - Bounding box to be checked for equality.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## bool EqualsNearly ( WorldBoundBox other , double epsilon )

Checks if the argument represents the same bounding box with regard to the specified accuracy (epsilon).
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **other** - Bounding box to be checked for equality.
- *double* **epsilon** - Epsilon value, that determines accuracy of comparison.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## bool Equals ( object obj )

Checks if the object and the bounding box are equal considering the predefined accuracy (epsilon).
### Arguments

- *[object](../../../../../api/library/objects/class.object_cs.md)* **obj** - Object.

### Return value

**true** if the size and position of the object and the bounding box are equal; otherwise, **false**.
## int GetHashCode ( )

Returns a hash code for the current object. Serves as the default hash function.
### Return value

Hash code.
## void SetTransform ( dmat4 transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void SetTransform ( WorldBoundSphere bs , dmat4 transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Expand ( dvec3 point )

Expands the current bounding box to enclose the given point.
### Arguments

- *dvec3* **point** - Point coordinates.

## void Expand ( dvec3[] points )

Expands the current bounding box to enclose all given points.
### Arguments

- *dvec3[]* **points** - Array of points to be enclosed by the bounding box.

## void Expand ( WorldBoundSphere bs )

Expands the current bounding box to enclose the given bounding sphere.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

## void Expand ( WorldBoundBox bb )

Expands the current bounding box to enclose the given bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

## bool Inside ( dvec3 point )

Checks if the given point is inside the bounding box.
### Arguments

- *dvec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool Inside ( dvec3 point , double radius )

Checks if the given sphere is inside the current bounding box.
### Arguments

- *dvec3* **point** - Coordinates of the center of the sphere.
- *double* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool inside ( dvec3 min_ , vec3 max_ )

Checks if the box with the given coordinates is inside the current bounding box.
### Arguments

- *dvec3* **min_** - Minimum coordinates of the box.
- *vec3* **max_** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( dvec3 point )


Checks if given point is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.


### Arguments

- *dvec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool InsideValid ( dvec3 point , double radius )

Checks if the sphere is inside the bounding box.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *dvec3* **point** - Coordinates of the center of the sphere.
- *double* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool InsideValid ( dvec3 min_ , dvec3 max_ )

Checks if the box specified in the argument is inside the current bound.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *dvec3* **min_** - Minimum coordinates of the box.
- *dvec3* **max_** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( dvec3[] points )

Checks if the points specified in the argument are inside the current bound.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *dvec3[]* **points** - Array of points.

### Return value

**true** if the specified points are inside the bounding box; otherwise, **false**.
## bool Inside ( WorldBoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding box.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool Inside ( WorldBoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( WorldBoundSphere bs )


Checks if the bounding sphere specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideValid ( WorldBoundBox bb )


Checks if the bounding box specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool InsideAll ( WorldBoundSphere bs )

Checks if the whole bounding sphere specified in the argument is inside the current bounding box.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideAll ( WorldBoundBox bb )

Checks if the whole bounding box specified in the argument is inside the current bounding box.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool InsideAllValid ( WorldBoundSphere bs )


Checks if the bounding sphere specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideAllValid ( WorldBoundBox bb )


Checks if the whole bounding box specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool InsideCube ( int face , dvec3 offset )

Checks if a face of the current bounding box is inside the cube represented by minimum and maximum coordinates of the bounding box.
### Arguments

- *int* **face** - The face index from **0** to **5**.
- *dvec3* **offset** - Offset.

### Return value

**true** if the face is inside the bounding cube; otherwise, **false**.
## bool RayIntersection ( dvec3 point , dvec3 direction )

Checks for an intersection between a ray and the current bound.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction vector coordinates.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool IRayIntersection ( dvec3 point , dvec3 idirection )

Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.
### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool GetIntersection ( dvec3 p0 , dvec3 p1 )

Checks for an intersection between a line and the current bounding box.
### Arguments

- *dvec3* **p0** - Starting point of the line.
- *dvec3* **p1** - Enging point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## bool RayIntersectionValid ( dvec3 point , dvec3 direction )


Checks for an intersection between a ray and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **direction** - Direction vector coordinates.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool IRayIntersectionValid ( dvec3 point , dvec3 idirection )


Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *dvec3* **point** - Starting point of the ray.
- *dvec3* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool GetIntersectionValid ( dvec3 p0 , dvec3 p1 )


Checks for an intersection between a line and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *dvec3* **p0** - Starting point of the line.
- *dvec3* **p1** - Ending point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## double Distance ( )

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance in units if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../../api/library/math/constants_cs.md)**.
## double Distance ( dvec3 point )

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *dvec3* **point** - Coordinates of a point.

### Return value

Distance in units if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../../api/library/math/constants_cs.md)**.
## double DistanceValid ( )


Returns the distance from the origin of coordinates to the closest vertex of the bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Return value

Resulting *double* value.
## double DistanceValid ( dvec3 point )


Returns the distance from the given point to the closest vertex of the bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *dvec3* **point** - Coordinates of a point.

### Return value

Resulting *double* value.
