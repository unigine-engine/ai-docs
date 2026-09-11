# Unigine.BoundBox Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding box in single precision coordinates.


Instances of this structure are deleted automatically, when necessary.


In case of double precision coordinates, the bounding box should be constructed by using the **[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)** structure. It includes the same functions as the *BoundBox* structure, but its functions deal with the double precision coordinates.


To support both single and double precision builds, you can use the *WorldBoundBox* structure only. The engine will automatically substitute it with the *BoundBox*, if required.


## BoundBox Class

### Members

---

## BoundBox ( vec3 min_ , vec3 max_ )

Constructor. Initializes the bounding box by the minimum and maximum coordinates.
### Arguments

- *vec3* **min_** - Minimum coordinates of the bounding box.
- *vec3* **max_** - Maximum coordinates of the bounding box.

## BoundBox ( vec3[] points )

Constructor. Initializes the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *vec3[]* **points** - Array of points to be enclosed by the bounding box.

## BoundBox ( BoundBox bb )

Constructor. Initializes the bounding box equal to the bounding box specified in the argument.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## BoundBox ( BoundBox bb , mat4 transform )

Constructor. Initializes the bounding box by the given bounding box with the given transformation matrix.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *mat4* **transform** - Transformation matrix.

## BoundBox ( BoundBox bb , dmat4 transform )

Constructor. Initializes the bounding box by the given bounding box with the given transformation matrix taken into account.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *dmat4* **transform** - Transformation matrix.

## BoundBox ( BoundSphere bs )

Constructor. Initializes the bounding box by the bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## BoundBox operator* ( mat4 m , BoundBox bs )

Multiplies the matrix by the bounding box and returns the resulting bounding box.
### Arguments

- *mat4* **m** - Matrix.
- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bs** - Bounding box.

### Return value

Resulting bounding box.
## BoundBox operator* ( dmat4 m , BoundBox bs )

Multiplies the matrix by the bounding box and returns the resulting bounding box.
### Arguments

- *dmat4* **m** - Matrix.
- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bs** - Bounding box.

### Return value

Bounding box.
## void Set ( vec3 min_ , vec3 max_ )

Sets the bounding box by the minimum and maximum coordinates.
### Arguments

- *vec3* **min_** - Minimum coordinates of the bounding box.
- *vec3* **max_** - Maximum coordinates of the bounding box.

## void Set ( vec3[] points )

Sets the bounding box by the coordinates of points in space to be enclosed by it.
### Arguments

- *vec3[]* **points** - Array of points to be enclosed by the bounding box.

## void Set ( BoundBox bb )

Sets the bounding box equal to the bounding box specified in the argument.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

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

## void Set ( BoundSphere bs )

Sets the bounding box by the bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## void Clear ( )

Clears the bounding box by setting all components/elements to 0.
## bool Equals ( BoundBox other )

Checks if the current bounding box is equal to the specified argument considering the predefined accuracy (epsilon).
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **other** - Bounding box to be checked for equality.

### Return value

**true** if the size and position of both bounding boxes are equal; otherwise, **false**.
## bool EqualsNearly ( BoundBox other , float epsilon )

Checks if the argument represents the same bounding box with regard to the specified accuracy (epsilon).
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **other** - Bounding box to be checked for equality.
- *float* **epsilon** - Epsilon value, that determines accuracy of comparison.

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
## void SetTransform ( mat4 transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void SetTransform ( dmat4 transform )

Sets the given transformation matrix to the bounding box.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void SetTransform ( BoundSphere bs , mat4 transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.
- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void SetTransform ( BoundSphere bs , dmat4 transform )

Sets the transformation matrix of the current bounding box for including the given bounding sphere with the given transformation matrix taken into account.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.
- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## void Expand ( vec3 point )

Expands the current bounding box to enclose the given point.
### Arguments

- *vec3* **point** - Point coordinates.

## void Expand ( vec3[] points )

Expands the current bounding box to enclose all given points.
### Arguments

- *vec3[]* **points** - Array of points to be enclosed by the bounding box.

## void Expand ( BoundSphere bs )

Expands the current bounding box to enclose the given bounding sphere.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

## void Expand ( BoundBox bb )

Expands the current bounding box to enclose the given bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

## bool Inside ( vec3 point )

Checks if the given point is inside the bounding box.
### Arguments

- *vec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool Inside ( vec3 point , float radius )

Checks if the given sphere is inside the current bounding box.
### Arguments

- *vec3* **point** - Coordinates of the center of the sphere.
- *float* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool inside ( vec3 min_ , vec3 max_ )

Checks if the box with the given coordinates is inside the current bounding box.
### Arguments

- *vec3* **min_** - Minimum coordinates of the box.
- *vec3* **max_** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( vec3 point )


Checks if given point is inside the bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.


### Arguments

- *vec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding box; otherwise, **false**.
## bool InsideValid ( vec3 point , float radius )

Checks if the sphere is inside the bounding box.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *vec3* **point** - Coordinates of the center of the sphere.
- *float* **radius** - Sphere radius.

### Return value

**true** if the sphere is inside the bounding box; otherwise, **false**.
## bool InsideValid ( vec3 min_ , vec3 max_ )

Checks if the box specified in the argument is inside the current bound.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *vec3* **min_** - Minimum coordinates of the box.
- *vec3* **max_** - Maximum coordinates of the box.

### Return value

**true** if the box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( vec3[] points )

Checks if the points specified in the argument are inside the current bound.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *vec3[]* **points** - Array of points.

### Return value

**true** if the specified points are inside the bounding box; otherwise, **false**.
## bool Inside ( BoundSphere bs )

Checks if the bounding sphere specified in the argument is inside the current bounding box.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool Inside ( BoundBox bb )

Checks if the bounding box specified in the argument is inside the current bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool InsideValid ( BoundSphere bs )


Checks if the bounding sphere specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideValid ( BoundBox bb )


Checks if the bounding box specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding box; otherwise, **false**.
## bool InsideAll ( BoundSphere bs )

Checks if the whole bounding sphere specified in the argument is inside the current bounding box.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideAll ( BoundBox bb )

Checks if the whole bounding box specified in the argument is inside the current bounding box.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool InsideAllValid ( BoundSphere bs )


Checks if the bounding sphere specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding box; otherwise, **false**.
## bool InsideAllValid ( BoundBox bb )


Checks if the whole bounding box specified in the argument is inside the current bounding box.


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bounding box are valid.


### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding box; otherwise, **false**.
## bool InsideCube ( int face , vec3 offset )

Checks if a face of the current bounding box is inside the cube represented by minimum and maximum coordinates of the bounding box.
### Arguments

- *int* **face** - The face index from **0** to **5**.
- *vec3* **offset** - Offset.

### Return value

**true** if the face is inside the bounding cube; otherwise, **false**.
## bool RayIntersection ( vec3 point , vec3 direction )

Checks for an intersection between a ray and the current bounding box.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction vector of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool IRayIntersection ( vec3 point , vec3 idirection )

Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.
### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool GetIntersection ( vec3 p0 , vec3 p1 )

Checks for an intersection between a line and the current bounding box.
### Arguments

- *vec3* **p0** - Starting point of the line.
- *vec3* **p1** - Enging point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## bool RayIntersectionValid ( vec3 point , vec3 direction )


Checks for an intersection between a ray and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **direction** - Direction vector of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool IRayIntersectionValid ( vec3 point , vec3 idirection )


Checks for an intersection between a ray and the current bounding box. This function uses the inverse direction of the ray, which increases performance.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *vec3* **point** - Starting point of the ray.
- *vec3* **idirection** - Inverse direction of the ray.

### Return value

**true** if the given ray intersects the bounding box; otherwise, **false**.
## bool GetIntersectionValid ( vec3 p0 , vec3 p1 )


Checks for an intersection between a line and the current bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *vec3* **p0** - Starting point of the line.
- *vec3* **p1** - Enging point of the line.

### Return value

**true** if the given line intersects the bounding box; otherwise, **false**.
## float Distance ( )

Returns the distance from the origin of coordinates to the closest vertex of the bounding box.
### Return value

Distance in units if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../../api/library/math/constants_cs.md)**.
## float Distance ( vec3 point )

Returns the distance from the given point to the closest vertex of the bounding box.
### Arguments

- *vec3* **point** - Coordinates of a point.

### Return value

Distance, in units, if the minimum and maximum coordinates of the bounding box are valid; otherwise, **[INF](../../../../../api/library/math/constants_cs.md)**.
## float DistanceValid ( )


Returns the distance from the origin of coordinates to the closest vertex of the bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Return value

Distance, in units.
## float DistanceValid ( vec3 point )


Returns the distance from the given point to the closest vertex of the bounding box.


> **Notice:** This function doesn't check if the minimum and maximum coordinates of the bounding box are valid.


### Arguments

- *vec3* **point** - Point.

### Return value

Distance, in units.
## bool IsCameraVisible ( vec3 camera , float min_distance , float max_distance )

Returns a value indicating if the bounding box is within the camera visibility distance.
### Arguments

- *vec3* **camera** - Coordinates of the camera position.
- *float* **min_distance** - Minimum visibility distance, in meters.
- *float* **max_distance** - Maximum visibility distance, in meters.

### Return value

**true** if the bounding box is within the camera visibility distance; otherwise, **false**.
