# Unigine.dmat4 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure represents a matrix of twelve (3x4) double components.


The dmat4 matrix is used for world transformations only (translation, scaling, rotation). This matrix isn't used for 3D projection, so its last row is skipped (that's why its size is 3x4 not 4x4). It allows avoiding high memory usage and performance loss when using the double precision coordinates.


The first, the second and the third columns of the matrix represent the rotation and the scale of the origin. The last column contains the translation of the origin relatively to the world origin.


![](../dmat4_matrix.png)


For any other purposes, the [mat4](../../../../api/library/math/class.mat4_cs.md) matrix can be used.


## dmat4 Class

### Properties

## 🔒︎ double m20

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ double m21

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ double m22

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ double m23

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ dmat4 ZERO

The Matrix, filled with zeros (0).
## 🔒︎ dmat4 ONE

The Matrix, filled with ones (1).
## 🔒︎ dmat4 IDENTITY

The Identity matrix.
## 🔒︎ dvec4 Row0

The First row.
## 🔒︎ dvec4 Row1

The Second row.
## 🔒︎ dvec4 Row2

The Third row.
## 🔒︎ dvec4 Row3

The Fourth row.
## 🔒︎ dvec4 Column0

The First column.
## 🔒︎ dvec4 Column1

The Second column.
## 🔒︎ dvec4 Column2

The Third column.
## 🔒︎ dvec4 Column3

The Fourth column.
## 🔒︎ dvec4 AxisX

The X axis.
## 🔒︎ dvec4 AxisY

The Y axis.
## 🔒︎ dvec4 AxisZ

The Z axis.
## 🔒︎ dvec4 AxisW

The W axis.
## 🔒︎ dvec3 Translate

The Translation part of the matrix. For more information see [Matrix Transformations](../../../../code/fundamentals/matrix_transformations/index_cs.md).
## 🔒︎ vec3 Scale

The Scaling part of the matrix. For more information see [Matrix Transformations](../../../../code/fundamentals/matrix_transformations/index_cs.md).
## 🔒︎ double Determinant

The Determinant of the matrix.
### Members

---

## bool operator== ( dmat4 v0 , dmat4 v1 )

Performs equal comparison.
### Arguments

- *dmat4* **v0** - First value.
- *dmat4* **v1** - Second value.

## bool operator!= ( dmat4 v0 , dmat4 v1 )

Not equal comparison.
### Arguments

- *dmat4* **v0** - First value.
- *dmat4* **v1** - Second value.

## bool Equals ( dmat4 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *dmat4* **other** - Value to be checked for equality.

### Return value

Return value.
## bool Equals ( object obj )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *[object](../../../../api/library/objects/class.object_cs.md)* **obj**

### Return value

Return value.
## int GetHashCode ( )

Returns a hash code for the current object. Serves as the default hash function.
### Return value

Resulting *int* value.
## dmat4 operator- ( dmat4 m )

Subtraction.
### Arguments

- *dmat4* **m** - Matrix.

## dmat4 operator* ( dmat4 m , double v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *double* **v** - Value.

## dvec2 operator* ( dmat4 m , vec2 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *vec2* **v** - Value.

## dvec2 operator* ( vec2 v , dmat4 m )

Multiplication.
### Arguments

- *vec2* **v** - Value.
- *dmat4* **m** - Matrix.

## dvec3 operator* ( dmat4 m , vec3 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *vec3* **v** - Value.

## dvec3 operator* ( vec3 v , dmat4 m )

Multiplication.
### Arguments

- *vec3* **v** - Value.
- *dmat4* **m** - Matrix.

## dvec4 operator* ( dmat4 m , vec4 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *vec4* **v** - Value.

## dvec4 operator* ( vec4 v , dmat4 m )

Multiplication.
### Arguments

- *vec4* **v** - Value.
- *dmat4* **m** - Matrix.

## dvec2 operator* ( dmat4 m , dvec2 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *dvec2* **v** - Value.

## dvec2 operator* ( dvec2 v , dmat4 m )

Multiplication.
### Arguments

- *dvec2* **v** - Value.
- *dmat4* **m** - Matrix.

## dvec3 operator* ( dmat4 m , dvec3 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *dvec3* **v** - Value.

## dvec3 operator* ( dvec3 v , dmat4 m )

Multiplication.
### Arguments

- *dvec3* **v** - Value.
- *dmat4* **m** - Matrix.

## dvec4 operator* ( dmat4 m , dvec4 v )

Multiplication.
### Arguments

- *dmat4* **m** - Matrix.
- *dvec4* **v** - Value.

## dvec4 operator* ( dvec4 v , dmat4 m )

Multiplication.
### Arguments

- *dvec4* **v** - Value.
- *dmat4* **m** - Matrix.

## dmat4 operator* ( dmat4 m0 , dmat4 m1 )

Multiplication.
### Arguments

- *dmat4* **m0** - Matrix 1.
- *dmat4* **m1** - Matrix 2.

## dmat4 operator+ ( dmat4 m0 , dmat4 m1 )

Addition.
### Arguments

- *dmat4* **m0** - Matrix 1.
- *dmat4* **m1** - Matrix 2.

## dmat4 operator- ( dmat4 m0 , dmat4 m1 )

Subtraction.
### Arguments

- *dmat4* **m0** - Matrix 1.
- *dmat4* **m1** - Matrix 2.

## void Set ( double m00_ , double m10_ , double m20_ , double m30_ , double m01_ , double m11_ , double m21_ , double m31_ , double m02_ , double m12_ , double m22_ , double m32_ , double m03_ , double m13_ , double m23_ , double m33_ )


Sets the value using the specified argument(s).


```text
Resulting matrix:
    | m00_  m01_  	m02_	 m03_ |
M=  | m10_  m11_  	m12_     m13_ |
    | m20_  m21_    m22_     m23_ |
    | m30_  m31_    m32_     m33_ |

```


### Arguments

- *double* **m00_** - m00_ element.
- *double* **m10_** - m10_ element.
- *double* **m20_** - m20_ element.
- *double* **m30_** - m30_ element.
- *double* **m01_** - m01_ element.
- *double* **m11_** - m11_ element.
- *double* **m21_** - m21_ element.
- *double* **m31_** - m31_ element.
- *double* **m02_** - m02_ element.
- *double* **m12_** - m12_ element.
- *double* **m22_** - m22_ element.
- *double* **m32_** - m32_ element.
- *double* **m03_** - m03_ element.
- *double* **m13_** - m13_ element.
- *double* **m23_** - m23_ element.
- *double* **m33_** - m33_ element.

## void Set ( double m00_ , double m10_ , double m20_ , double m01_ , double m11_ , double m21_ , double m02_ , double m12_ , double m22_ , double m03_ , double m13_ , double m23_ )

Sets the value using the specified argument(s).
### Arguments

- *double* **m00_** - m00_ element.
- *double* **m10_** - m10_ element.
- *double* **m20_** - m20_ element.
- *double* **m01_** - m01_ element.
- *double* **m11_** - m11_ element.
- *double* **m21_** - m21_ element.
- *double* **m02_** - m02_ element.
- *double* **m12_** - m12_ element.
- *double* **m22_** - m22_ element.
- *double* **m03_** - m03_ element.
- *double* **m13_** - m13_ element.
- *double* **m23_** - m23_ element.

## void Set ( double v )

Sets the value using the specified argument(s).
### Arguments

- *double* **v** - A *double* value to be used.

## void Set ( mat2 m )

Sets the value using the specified argument(s).
### Arguments

- *mat2* **m** - Source matrix.

## void Set ( mat3 m )

Sets the value using the specified argument(s).
### Arguments

- *mat3* **m** - Source matrix.

## void Set ( mat4 m )

Sets the value using the specified argument(s).
### Arguments

- *mat4* **m** - Source matrix.

## void Set ( dmat4 m )

Sets the value using the specified argument(s).
### Arguments

- *dmat4* **m** - Source matrix.

## void Set ( dvec3 col0 , dvec3 col1 , dvec3 col2 , dvec3 col3 )

Sets the value using the specified argument(s).
### Arguments

- *dvec3* **col0** - First column.
- *dvec3* **col1** - Second column.
- *dvec3* **col2** - Third column.
- *dvec3* **col3** - Fourth column.

## void Set ( quat q )

Sets the value using the specified argument(s).
### Arguments

- *quat* **q** - Source quaternion.

## void Set ( mat3 m , dvec3 v )

Sets the value using the specified argument(s).
### Arguments

- *mat3* **m** - Source matrix.
- *dvec3* **v** - Source vector.

## void Set ( quat q , dvec3 v )

Sets the value using the specified argument(s).
### Arguments

- *quat* **q** - Source quaternion.
- *dvec3* **v** - Source vector.

## void Set ( float[] m , bool transpose )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **m** - Source matrix.
- *bool* **transpose** -  true - to transpose the resulting matrix, false -not to transpose.

## void Set ( double[] m , bool transpose )

Sets the value using the specified argument(s).
### Arguments

- *double[]* **m** - Source matrix.
- *bool* **transpose** -  true - to transpose the resulting matrix, false -not to transpose.

## void Set ( int row , int column , double v )

Sets the value using the specified argument(s).
### Arguments

- *int* **row** - Row index.
- *int* **column** - Column index.
- *double* **v** - A *double* value to be used.

## double Get ( int row , int column )

Returns the matrix element specified by the given row and column.
### Arguments

- *int* **row** - Row index.
- *int* **column** - Column index.

### Return value

Resulting *double* value.
## void Clear ( )

Clears the value by setting all components/elements to 0.
## void SetZero ( )

Sets all matrix elements equal to **0**.
## void SetIdentity ( )

Sets the matrix equal to the identity matrix.
## void SetRotate ( dvec3 axis , double angle )

Sets the rotation matrix for a given axis.
### Arguments

- *dvec3* **axis** - Axis of rotation.
- *double* **angle** - Angle, in degrees.

## quat GetRotate ( )

Returns the [quaternion](../../../../api/library/math/class.quat_cs.md), representing the rotation part of the matrix.
### Return value

Resulting rotation matrix.
## void SetRotateX ( double angle )

Sets X rotation matrix.
### Arguments

- *double* **angle** - Angle, in degrees.

## void SetRotateY ( double angle )

Sets Y rotation matrix.
### Arguments

- *double* **angle** - Angle, in degrees.

## void SetRotateZ ( double angle )

Sets Z rotation matrix.
### Arguments

- *double* **angle** - Angle, in degrees.

## void SetRow ( int row , dvec4 v )

Sets the specified row of the matrix using a given [dvec4](../../../../api/library/math/class.dvec4_cs.md) vector as a source.
### Arguments

- *int* **row** - Row index.
- *dvec4* **v** - Source vector.

## void SetRow3 ( int row , dvec3 v )

Sets the specified row of the matrix using a given three-component [dvec3](../../../../api/library/math/cs/dvec3_cs.md) vector as a source, the last element of the row remains as is.
### Arguments

- *int* **row** - Row index.
- *dvec3* **v** - Source vector.

## dvec4 GetRow ( int row )

Returns the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

Return value.
## dvec3 GetRow3 ( int row )

Returns the first three elements of the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

The [dvec3](../../../../api/library/math/cs/dvec3_cs.md) vector with the first three elements of the specified matrix row.
## void SetColumn ( int column , dvec4 v )

Sets the specified column of the matrix using a given [dvec4](../../../../api/library/math/cs/dvec4_cs.md) vector as a source.
### Arguments

- *int* **column** - Column index.
- *dvec4* **v** - Source vector.

## void SetColumn3 ( int column , dvec3 v )

Sets the specified column of the matrix using a given three-component [dvec3](../../../../api/library/math/cs/dvec3_cs.md) vector as a source.
### Arguments

- *int* **column** - Column index.
- *dvec3* **v** - Source vector.

## dvec4 GetColumn ( int column )

Returns the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

The [dvec4](../../../../api/library/math/cs/vec4_cs.md) vector with column values.
## dvec3 GetColumn3 ( int column )

Returns the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

The [dvec3](../../../../api/library/math/cs/dvec3_cs.md) vector with column values.
## string ToString ( )

Converts the current value to a *string* value.
### Return value

Resulting *string* value.
