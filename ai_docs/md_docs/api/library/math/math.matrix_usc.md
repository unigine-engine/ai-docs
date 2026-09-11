# Math Matrix Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a collection of matrix functions.


## Math Class

### Members

---

## mat4 cubeTransform ( int face )

Returns a transformation matrix (cube viewing matrix) for the specified face of a cube map. Cube maps are often used in rendering for environment mapping, reflection, or skyboxes. Each face of a cube map corresponds to one of the six directions: positive and negative X, Y, and Z axes.
### Arguments

- *int* **face** - Face number, one of the following: 0 (X+), 1 (X-), 2 (Y+), 3 (Y-), 4 (Z+),5 (Z-).

### Return value

Cube viewing matrix.
## mat4 frustum ( float left , float right , float bottom , float top , float znear , float zfar )


Returns perspective projection matrix:


| 2.0 * znear / (right - left) | 0.0 | (right + left) / (right - left) | 0.0 |
|---|---|---|---|
| 0.0 | 2.0 * znear / (top - bottom) | (top + bottom) / (top - bottom) | 0.0 |
| 0.0 | 0.0 | -(zfar + znear) / (zfar - znear) | -2.0 * zfar * znear / (zfar - znear) |
| 0.0 | 0.0 | -1.0 | 0.0 |


Coordinates of top, left, right, bottom are set relatively to center point of the znear plane.


![](frustum_desc.png)


There are two different points (A and B) on the picture above. Since the top, left, right, bottom are coordinates relatively to the center point of the znear plane, coordinates of the A point should be *A(left, bottom, znear)*. Coordinates of the B point are *B(k * left, k * bottom, zfar)*, where *k = zfar/znear.*


### Arguments

- *float* **left** - Left coordinate of the near clipping plane relatively to the center.
- *float* **right** - Right coordinate of the near clipping plane relatively to the center.
- *float* **bottom** - Bottom coordinate of the near clipping plane relatively to the center.
- *float* **top** - Top coordinate of the near clipping plane relatively to the center.
- *float* **znear** - Distance to the near depth clipping plane.
- *float* **zfar** - Distance to the farther depth clipping plane.

### Return value

Perspective projection matrix.
## Variable inverse ( Variable matrix )

Returns inverse of a matrix. Supports *mat3*, *mat4* and *dmat4* arguments. The inverse of a matrix is a matrix that if multiplied by the original would result in identity matrix: AA -1 = A -1A = I.
### Arguments

- *Variable* **matrix** - Matrix to be inverted (*mat3*, *mat4* or *dmat4*).

### Return value

Inverse of the matrix.
## quat inverse ( quat q )

Returns inverse of a quaternion. The inverse of a quaternion is a quaternion that if multiplied by the original would result in identity matrix: qq -1 = 1. If **q = a + bi + cj + dk**, then **q-1 = a - bi - cj - dk**
### Arguments

- *quat* **q** - Quaternion to be inverted.

### Return value

Inverse of the quaternion.
## Variable inverse4 ( mat4 matrix )


Inverts a matrix that consists of a 3�4 sub-matrix (upper left) and a translation vector. The last row of the matrix is ignored. Compared to the [inverse()](#inverse_variable) function, this one is a bit faster and, which is more important, more stable. A matrix suitable for such inversion looks like this:


| *m00* | *m10* | *m20* | *m30* |
|---|---|---|---|
| *m01* | *m11* | *m21* | *m31* |
| *m02* | *m12* | *m22* | *m32* |
| 0 | 0 | 0 | 1 |


### Arguments

- *mat4* **matrix** - Matrix to be inverted.

### Return value

Inverse of the matrix.
## Variable obliqueProjection ( mat4 projection , vec4 plane )

Returns the oblique projection matrix for the specified projection matrix to account for the specified clipping plane. This type of projection is known as oblique projection because it "clips" objects based on an arbitrary plane in space, not necessarily aligned with the view frustum. This can be useful for advanced rendering techniques like reflections or stenciling, where you may want to clip the scene or reflect it across a specific plane.
### Arguments

- *mat4* **projection** - Input projection matrix.
- *vec4* **plane** - A 4D vector representing the equation of the clipping plane (a, b, c, d), the plane equation is ax + by + cz + d = 0.

### Return value

Oblique projection matrix.
## Variable orthoTangent ( vec3 tangent , vec3 binormal , vec3 normal )


Calculates the tangent space basis basing on the 3 given ortho basis vectors.


> **Notice:** The **w** component will contain the sign of the binormal.


### Arguments

- *vec3* **tangent** - Tangent vector.
- *vec3* **binormal** - Binormal vector.
- *vec3* **normal** - Normal vector.

### Return value

Tangent space basis.
### Examples


The following example demonstrates how to convert the mesh tangent vector to the normal and binormal vectors. The mesh tangent vector is calculated via the *orthoTangent()* function.


```cpp
vec3 t = vec3(1.0f,0.0f,0.0f); // the tangent basis: tangent vector
vec3 b = vec3(0.0f,1.0f,0.0f); // binormal vector
vec3 n = vec3(0.0f,0.0f,1.0f); // normal vector
vec4 tangent = orthoTangent(t,b,n); // this is the mesh compressed tangent vector

quat compact_tangent_quat = quat(tangent); // convert vec4 to quat

log.message("b: %s\n",typeinfo(compact_tangent_quat.binormal)); // get the col1 (binormal) with w normalization
log.message("n: %s\n\n",typeinfo(compact_tangent_quat.normal)); // get the col2 (normal) with w normalization

// manually normalize the w component of the quaternion
// and convert the quaternion into the matrix
mat4 compact_tangent_mat = mat4(normalize3(compact_tangent_quat)); // when the w component of the quaternion is normalized, the sign of binormal will be lost for the matrix

// get the col1 and col2 of the matrix
log.message("b: %s\n",typeinfo(compact_tangent_mat.binormal * tangent.w)); // you should multiply the binormal by the tangent w component to restore the sign
log.message("n: %s\n",typeinfo(compact_tangent_mat.normal));

```


## Variable orthoTangent ( vec4 tangent , vec3 normal )


Calculates the tangent space basis basing on the given ortho basis vectors.


> **Notice:** The **w** component will contain the sign of the binormal.


### Arguments

- *vec4* **tangent** - Tangent vector: the first 3 components are coordinates of the tangent vector, and the fourth **w** component is the sign of the binormal.
- *vec3* **normal** - Normal vector.

### Return value

Tangent space basis.
## mat4 ortho ( float left , float right , float bottom , float top , float znear , float zfar )


Returns parallel projection matrix:


| 2.0 / (right - left) | 0.0 | 0.0 | -(right + left) / (right - left) |
|---|---|---|---|
| 0.0 | 2.0 / (top - bottom) | 0.0 | -(top + bottom) / (top - bottom) |
| 0.0 | 0.0 | -2.0 / (zfar - znear) | -(zfar + znear) / (zfar - znear) |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **left** - Left vertical clipping plane.
- *float* **right** - Right vertical clipping plane.
- *float* **bottom** - Bottom horizontal clipping plane.
- *float* **top** - Top horizontal clipping plane.
- *float* **znear** - Nearest depth clipping plane.
- *float* **zfar** - Farther depth clipping plane.

### Return value

Parallel projection matrix.
## bool isOrthoProjection ( )

Returns a value indicating if the specified projection matrix represents an orthographic projection.
### Arguments

### Return value

true if there is the specified projection matrix represents an orthographic projection, otherwise false.
## bool isPerspectiveProjection ( )

Returns a value indicating if the specified projection matrix represents a perspective projection.
### Arguments

### Return value

true if there is the specified projection matrix represents a perspective projection, otherwise false.
## mat4 perspective ( float fov , float aspect , float znear , float zfar )

Returns perspective projection matrix.
### Arguments

- *float* **fov** - Field of view angle.
- *float* **aspect** - Aspect ratio. The aspect ratio is the ratio of width to height.
- *float* **znear** - Nearest depth clipping plane.
- *float* **zfar** - Farther depth clipping plane.

### Return value

Perspective projection matrix.
## mat4 & removeScale ( )

Resets the transformation scale by replacing the scale component of the transformation matrix with a vec3_one (vector filled with ones). The original scale is stored in the vector argument.
### Arguments

### Return value

Output matrix.
## mat4 & removeScale ( )

Resets the transformation scale by replacing the scale component of the transformation matrix with a vec3_one (vector filled with ones).
### Arguments

### Return value

Output matrix.
## dmat4 & removeScale ( )

Resets the transformation scale by replacing the scale component of the transformation matrix with a vec3_one (vector filled with ones). The original scale is stored in the vector argument.
### Arguments

### Return value

Output matrix.
## dmat4 & removeScale ( )

Resets the transformation scale by replacing the scale component of the transformation matrix with a vec3_one (vector filled with ones).
### Arguments

### Return value

Output matrix.
## mat4 rotateX ( float angle )


Returns rotation matrix for the given angle around X axis:


| 1.0 | 0.0 | 0.0 | 0.0 |
|---|---|---|---|
| 0.0 | cos | -sin | 0.0 |
| 0.0 | sin | cos | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## mat4 rotateY ( float angle )


Returns rotation matrix for the given angle around Y axis:


| cos | 0.0 | sin | 0.0 |
|---|---|---|---|
| 0.0 | 1.0 | 0.0 | 0.0 |
| -sin | 0.0 | cos | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## mat4 rotateZ ( float angle )


Returns rotation matrix for the given angle around Z axis:


| cos | -sin | 0.0 | 0.0 |
|---|---|---|---|
| sin | cos | 0.0 | 0.0 |
| 0.0 | 0.0 | 1.0 | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## mat4 rotate ( float x , float y , float z , float angle )

Returns rotation matrix for the given angle around the given axis (X, Y, Z).
### Arguments

- *float* **x** - X component of rotation axis.
- *float* **y** - Y component of rotation axis.
- *float* **z** - Z component of rotation axis.
- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## mat4 rotate ( vec3 axis , float angle )

Returns rotation matrix for the given angle around the given axis (X, Y, Z).
### Arguments

- *vec3* **axis** - Rotation axis. This vector does not have to be normalized.
- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## Variable rotateTowards ( Variable source , Variable target , float max_angle )

Rotates the **source** vector towards the **target** vector by an angular step of **max_angle** (note, that the rotation will not overshoot).
### Arguments

- *Variable* **source** - Source vector/quaternion. Can be of the following types:

  - [vec3](../../../api/library/math/class.vec3_usc.md)
  - [quat](../../../api/library/math/class.quat_usc.md)
- *Variable* **target** - Target vector/quaternion. Can be of the following types:

  - [vec3](../../../api/library/math/class.vec3_usc.md)
  - [quat](../../../api/library/math/class.quat_usc.md)
- *float* **max_angle** - Angular step, in degrees. If a negative value is specified, 0 will be used instead.

### Return value


Resulting vector/quaternion. The type of return value depends on the argument type:


- [vec3](../../../api/library/math/class.vec3_usc.md) for *vec3* arguments
- [quat](../../../api/library/math/class.quat_usc.md) for *quat* arguments


## Variable rotation ( Variable v )

Returns the rotation matrix of the input source, supports *quat*, *mat4* and *dmat4* arguments. For more information see [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md).
### Arguments

- *Variable* **v** - Source, can be of *quat*, *mat4* or *dmat4* type.

### Return value

Rotation matrix.
## rotationFromDir ( )

Returns the rotation quaternion for the specified "forward" and "up" directions. For more information see [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md).
### Arguments

### Return value

## rotationFromDir ( )

Returns the rotation quaternion for the specified "forward" direction (the default "up" vector is used). For more information see [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md).
### Arguments

### Return value

## rotationFromTo ( const vec3 & from_dir , const vec3 & to_dir )

Returns the rotation quaternion for the specified source and target directions. For more information see [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_usc.md).
### Arguments

- *const vec3 &* **from_dir** - Vector defining the initial direction.
- *const vec3 &* **to_dir** - Vector defining the target direction.

### Return value

## mat4 scale ( float x , float y , float z )


Returns scaling matrix for the specified scaling vector (X, Y, Z):


| X | 0.0 | 0.0 | 0.0 |
|---|---|---|---|
| 0.0 | Y | 0.0 | 0.0 |
| 0.0 | 0.0 | Z | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **x** - X component of the scaling vector.
- *float* **y** - Y component of the scaling vector.
- *float* **z** - Z component of the scaling vector.

### Return value

Scaling matrix.
## mat4 scale ( vec3 vector )


Returns scaling matrix for the specified scaling vector (X, Y, Z):


| X | 0.0 | 0.0 | 0.0 |
|---|---|---|---|
| 0.0 | Y | 0.0 | 0.0 |
| 0.0 | 0.0 | Z | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *vec3* **vector** - Scaling vector.

### Return value

Scaling matrix.
## Variable translate ( Variable v )


Returns translation matrix:


| 1.0 | 0.0 | 0.0 | X |
|---|---|---|---|
| 0.0 | 1.0 | 0.0 | Y |
| 0.0 | 0.0 | 1.0 | Z |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *Variable* **v** - Translation vector (either *vec3* or *dvec3*).

### Return value


Translation matrix:


- *mat4*, if the input argument is *vec3*
- *dmat4* if the argument is *dvec3*


## Variable translate ( Variable x , Variable y , Variable z )


Returns the translation matrix:


| 1.0 | 0.0 | 0.0 | X |
|---|---|---|---|
| 0.0 | 1.0 | 0.0 | Y |
| 0.0 | 0.0 | 1.0 | Z |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *Variable* **x** - X component of the translation vector (*int*, *float* or *double*).
- *Variable* **y** - Y component of the translation vector (*int*, *float* or *double*).
- *Variable* **z** - Z component of the translation vector (*int*, *float* or *double*).

### Return value


Translation matrix:


- *mat4*, if the first input argument is *int* or *float*
- *dmat4*, if the first argument is *double*


## mat4 transpose ( mat4 matrix )


Returns the transpose matrix of the input matrix:


| m00 | m10 | m20 | m30 |
|---|---|---|---|
| m01 | m11 | m21 | m31 |
| m02 | m12 | m22 | m32 |
| m03 | m13 | m23 | m33 |


### Arguments

- *mat4* **matrix** - Argument.

### Return value

Transposed matrix.
## Variable transpose3 ( mat4 matrix )

Transposes the upper left 3�3 sub-matrix of a matrix.
### Arguments

- *mat4* **matrix** - Matrix, a part of which will be transposed.

### Return value

*Matrix*, in which the upper left 3�3 sub-matrix is transposed.
