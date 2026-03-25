# Unigine.mat4 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## mat4 Class

### Properties

## 🔒︎ float m00

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m10

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m20

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m30

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m01

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m11

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m21

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m31

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m02

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m12

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m22

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m32

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m03

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m13

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m23

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m33

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ mat4 ZERO

The Matrix, filled with zeros (0).
## 🔒︎ mat4 ONE

The Matrix, filled with ones (1).
## 🔒︎ mat4 IDENTITY

The Identity matrix.
## 🔒︎ vec4 Row0

The First row.
## 🔒︎ vec4 Row1

The Second row.
## 🔒︎ vec4 Row2

The Third row.
## 🔒︎ vec4 Row3

The Fourth row.
## 🔒︎ vec4 Column0

The First column.
## 🔒︎ vec4 Column1

The Second column.
## 🔒︎ vec4 Column2

The Third column.
## 🔒︎ vec4 Column3

The Fourth column.
## 🔒︎ vec4 AxisX

The X axis.
## 🔒︎ vec4 AxisY

The Y axis.
## 🔒︎ vec4 AxisZ

The Z axis.
## 🔒︎ vec4 AxisW

The W axis.
## 🔒︎ vec4 Diagonal

The Vector containing diagonal elements of the matrix.
## 🔒︎ vec3 Translate

The Translation part of the matrix. For more information see [Matrix Transformations](../../../../code/fundamentals/matrix_transformations/index_cs.md).
## 🔒︎ vec3 Scale

The Scaling part of the matrix. For more information see [Matrix Transformations](../../../../code/fundamentals/matrix_transformations/index_cs.md).
## 🔒︎ float Trace

The Trace of the matrix: (sum of its diagonal elements).
## 🔒︎ float Determinant

The Determinant of the matrix.
## 🔒︎ float Determinant3

The Determinant of the smaller 3x3 matrix.
### Members

---

## bool operator== ( mat4 v0 , mat4 v1 )

Performs equal comparison.
### Arguments

- *mat4* **v0** - First value.
- *mat4* **v1** - Second value.

## bool operator!= ( mat4 v0 , mat4 v1 )

Not equal comparison.
### Arguments

- *mat4* **v0** - First value.
- *mat4* **v1** - Second value.

## bool Equals ( mat4 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *mat4* **other** - Value to be checked for equality.

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
## mat4 operator- ( mat4 m )

Subtraction.
### Arguments

- *mat4* **m** - Matrix.

## mat4 operator* ( mat4 m , float v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *float* **v** - Value.

## vec2 operator* ( mat4 m , vec2 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *vec2* **v** - Value.

## vec2 operator* ( vec2 v , mat4 m )

Multiplication.
### Arguments

- *vec2* **v** - Value.
- *mat4* **m** - Matrix.

## vec3 operator* ( mat4 m , vec3 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *vec3* **v** - Value.

## vec3 operator* ( vec3 v , mat4 m )

Multiplication.
### Arguments

- *vec3* **v** - Value.
- *mat4* **m** - Matrix.

## vec4 operator* ( mat4 m , vec4 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *vec4* **v** - Value.

## vec4 operator* ( vec4 v , mat4 m )

Multiplication.
### Arguments

- *vec4* **v** - Value.
- *mat4* **m** - Matrix.

## dvec2 operator* ( mat4 m , dvec2 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *dvec2* **v** - Value.

## dvec2 operator* ( dvec2 v , mat4 m )

Multiplication.
### Arguments

- *dvec2* **v** - Value.
- *mat4* **m** - Matrix.

## dvec3 operator* ( mat4 m , dvec3 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *dvec3* **v** - Value.

## dvec3 operator* ( dvec3 v , mat4 m )

Multiplication.
### Arguments

- *dvec3* **v** - Value.
- *mat4* **m** - Matrix.

## dvec4 operator* ( mat4 m , dvec4 v )

Multiplication.
### Arguments

- *mat4* **m** - Matrix.
- *dvec4* **v** - Value.

## dvec4 operator* ( dvec4 v , mat4 m )

Multiplication.
### Arguments

- *dvec4* **v** - Value.
- *mat4* **m** - Matrix.

## mat4 operator* ( mat4 m0 , mat4 m1 )

Multiplication.
### Arguments

- *mat4* **m0** - First value.
- *mat4* **m1** - Second value.

## mat4 operator+ ( mat4 m0 , mat4 m1 )

Addition.
### Arguments

- *mat4* **m0** - First value.
- *mat4* **m1** - Second value.

## mat4 operator- ( mat4 m0 , mat4 m1 )

Subtraction.
### Arguments

- *mat4* **m0** - First value.
- *mat4* **m1** - Second value.

## void Set ( float m00_ , float m10_ , float m20_ , float m30_ , float m01_ , float m11_ , float m21_ , float m31_ , float m02_ , float m12_ , float m22_ , float m32_ , float m03_ , float m13_ , float m23_ , float m33_ )

Sets the value using the specified argument(s).
### Arguments

- *float* **m00_** - m00_ element.
- *float* **m10_** - m10_ element.
- *float* **m20_** - m20_ element.
- *float* **m30_** - m30_ element.
- *float* **m01_** - m01_ element.
- *float* **m11_** - m11_ element.
- *float* **m21_** - m21_ element.
- *float* **m31_** - m31_ element.
- *float* **m02_** - m02_ element.
- *float* **m12_** - m12_ element.
- *float* **m22_** - m22_ element.
- *float* **m32_** - m32_ element.
- *float* **m03_** - m03_ element.
- *float* **m13_** - m13_ element.
- *float* **m23_** - m23_ element.
- *float* **m33_** - m33_ element.

## void Set ( float v )

Sets the value using the specified argument(s).
### Arguments

- *float* **v** - A *float* value to be used.

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

## void Set ( vec4 col0 , vec4 col1 , vec4 col2 , vec4 col3 )

Sets the value using the specified argument(s).
### Arguments

- *vec4* **col0** - First column.
- *vec4* **col1** - Second column.
- *vec4* **col2** - Third column.
- *vec4* **col3** - Fourth column.

## void Set ( quat q )

Sets the value using the specified argument(s).
### Arguments

- *quat* **q** - Source quaternion.

## void Set ( mat3 m , vec3 v )

Sets the value using the specified argument(s).
### Arguments

- *mat3* **m** - Source matrix.
- *vec3* **v** - Source vector.

## void Set ( quat q , vec3 v )

Sets the value using the specified argument(s).
### Arguments

- *quat* **q** - Source quaternion.
- *vec3* **v** - Source vector.

## void Set ( float[] m , bool transpose )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **m** - Source matrix.
- *bool* **transpose** -  true - to transpose the resulting matrix, false -not to transpose.

## void SetRow ( int row , vec4 v )

Sets the specified row of the matrix using a given [vec4](../../../../api/library/math/cs/vec4_cs.md) vector as a source.
### Arguments

- *int* **row** - Row index.
- *vec4* **v** - Source vector.

## void SetRow3 ( int row , vec3 v )

Sets the specified row of the matrix using a given three-component [vec3](../../../../api/library/math/cs/vec3_cs.md) vector as a source, the last element of the row remains as is.
### Arguments

- *int* **row** - Row index.
- *vec3* **v** - Source vector.

## vec4 GetRow ( int row )

Returns the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

Return value.
## vec3 GetRow3 ( int row )

Returns the first three elements of the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

Return value.
## void SetColumn ( int column , vec4 v )

Sets the specified column of the matrix using a given [vec4](../../../../api/library/math/cs/vec4_cs.md) vector as a source.
### Arguments

- *int* **column** - Column index.
- *vec4* **v** - Source vector.

## void SetColumn3 ( int column , vec3 v )

Sets the specified column of the matrix using a given three-component [vec3](../../../../api/library/math/cs/vec3_cs.md) vector as a source, the last element of the column remains as is.
### Arguments

- *int* **column** - Column index.
- *vec3* **v** - Source vector.

## vec4 GetColumn ( int column )

Returns the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

Return value.
## vec3 GetColumn3 ( int column )

Returns the XYZ components of the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

Return value.
## void Clear ( )

Clears the value by setting all components/elements to 0.
## void SetZero ( )

Sets all matrix elements equal to **0**.
## void SetIdentity ( )

Sets the matrix equal to the identity matrix.
## void SetRotate ( vec3 axis , float angle )

Sets the rotation matrix for a given axis.
### Arguments

- *vec3* **axis** - Axis of rotation.
- *float* **angle** - Angle, in degrees.

## quat GetRotate ( )

Returns the [quaternion](../../../../api/library/math/cs/quat_cs.md), representing the rotation part of the matrix.
### Return value

Resulting rotation matrix.
## void SetRotateX ( float angle )

Sets X rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## void SetRotateY ( float angle )

Sets Y rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## void SetRotateZ ( float angle )

Set Z rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## string ToString ( )

Converts the current value to a *string* value.
### Return value

Resulting *string* value.
