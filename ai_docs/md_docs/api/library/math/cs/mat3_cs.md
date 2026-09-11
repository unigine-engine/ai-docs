# Unigine.mat3 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## mat3 Class

### Properties

## 🔒︎ float m00

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m10

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m20

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m01

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m11

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m21

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m02

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m12

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m22

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ mat3 ZERO

The Matrix, filled with zeros (0).
## 🔒︎ mat3 ONE

The Matrix, filled with ones (1).
## 🔒︎ mat3 IDENTITY

The Identity matrix.
## 🔒︎ quat Quat

The Quaternion that this matrix represents.
## 🔒︎ vec3 Row0

The First row.
## 🔒︎ vec3 Row1

The Second row.
## 🔒︎ vec3 Row2

The Third row.
## 🔒︎ vec3 Column0

The First column.
## 🔒︎ vec3 Column1

The Second column.
## 🔒︎ vec3 Column2

The Third column.
## 🔒︎ vec3 AxisX

The X axis.
## 🔒︎ vec3 AxisY

The Y axis.
## 🔒︎ vec3 AxisZ

The Z axis.
## 🔒︎ vec3 Diagonal

The Vector containing diagonal elements of the matrix.
## 🔒︎ float Trace

The Trace of the matrix: (sum of its diagonal elements).
## 🔒︎ float Determinant

The Determinant of the matrix.
### Members

---

## bool operator== ( mat3 v0 , mat3 v1 )

Performs equal comparison.
### Arguments

- *mat3* **v0** - First value.
- *mat3* **v1** - Second value.

## bool operator!= ( mat3 v0 , mat3 v1 )

Not equal comparison.
### Arguments

- *mat3* **v0** - First value.
- *mat3* **v1** - Second value.

## bool Equals ( mat3 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *mat3* **other** - Value to be checked for equality.

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
## mat3 operator- ( mat3 m )

Subtraction.
### Arguments

- *mat3* **m** - Matrix.

## mat3 operator* ( mat3 m , float v )

Multiplication.
### Arguments

- *mat3* **m** - Matrix.
- *float* **v** - Value.

## vec2 operator* ( mat3 m , vec2 v )

Multiplication.
### Arguments

- *mat3* **m** - Matrix.
- *vec2* **v** - Value.

## vec2 operator* ( vec2 v , mat3 m )

Multiplication.
### Arguments

- *vec2* **v** - Value.
- *mat3* **m** - Matrix.

## vec3 operator* ( mat3 m , vec3 v )

Multiplication.
### Arguments

- *mat3* **m** - Matrix.
- *vec3* **v** - Value.

## vec3 operator* ( vec3 v , mat3 m )

Multiplication.
### Arguments

- *vec3* **v** - Value.
- *mat3* **m** - Matrix.

## dvec2 operator* ( mat3 m , dvec2 v )

Multiplication.
### Arguments

- *mat3* **m** - Matrix.
- *dvec2* **v** - Value.

## dvec2 operator* ( dvec2 v , mat3 m )

Multiplication.
### Arguments

- *dvec2* **v** - Value.
- *mat3* **m** - Matrix.

## dvec3 operator* ( mat3 m , dvec3 v )

Multiplication.
### Arguments

- *mat3* **m** - Matrix.
- *dvec3* **v** - Value.

## dvec3 operator* ( dvec3 v , mat3 m )

Multiplication.
### Arguments

- *dvec3* **v** - Value.
- *mat3* **m** - Matrix.

## mat3 operator* ( mat3 m0 , mat3 m1 )

Multiplication.
### Arguments

- *mat3* **m0** - First value.
- *mat3* **m1** - Second value.

## mat3 operator+ ( mat3 m0 , mat3 m1 )

Addition.
### Arguments

- *mat3* **m0** - First value.
- *mat3* **m1** - Second value.

## mat3 operator- ( mat3 m0 , mat3 m1 )

Subtraction.
### Arguments

- *mat3* **m0** - First value.
- *mat3* **m1** - Second value.

## void Set ( float m00_ , float m10_ , float m20_ , float m01_ , float m11_ , float m21_ , float m02_ , float m12_ , float m22_ )


Sets the value using the specified argument(s).


```text
Resulting matrix:
    | m00_	 m01_	m02_ |
M=  | m10_   m11_   m12_ |
    | m20_   m21_   m22_ |

```


### Arguments

- *float* **m00_** - m00_ element.
- *float* **m10_** - m10_ element.
- *float* **m20_** - m20_ element.
- *float* **m01_** - m01_ element.
- *float* **m11_** - m11_ element.
- *float* **m21_** - m21_ element.
- *float* **m02_** - m02_ element.
- *float* **m12_** - m12_ element.
- *float* **m22_** - m22_ element.

## void Set ( float v )

Sets the value using the specified argument(s).
### Arguments

- *float* **v** - A *float* value to be used.

## void Set ( float[] m )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **m** - Source matrix.

## void Set ( mat3 m )

Sets the value using the specified argument(s).
### Arguments

- *mat3* **m** - Source matrix.

## void Set ( mat2 m )

Sets the value using the specified argument(s).
### Arguments

- *mat2* **m** - Source matrix.

## void Set ( mat4 m )

Sets the value using the specified argument(s).
### Arguments

- *mat4* **m** - Source matrix.

## void Set ( dmat4 m )

Sets the value using the specified argument(s).
### Arguments

- *dmat4* **m** - Source matrix.

## void Set ( vec3 col0 , vec3 col1 , vec3 col2 )

Sets the value using the specified argument(s).
### Arguments

- *vec3* **col0** - First column.
- *vec3* **col1** - Second column.
- *vec3* **col2** - Third column.

## void Set ( quat q )

Sets the value using the specified argument(s).
### Arguments

- *quat* **q** - Source quaternion.

## void SetRow ( int row , vec3 v )

Sets the specified row of the matrix using a given [vec3](../../../../api/library/math/cs/vec3_cs.md) vector as a source.
### Arguments

- *int* **row** - Row index.
- *vec3* **v** - Source vector.

## vec3 GetRow ( int row )

Returns the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

Return value.
## void SetColumn ( int column , vec3 v )

Sets the specified column of the matrix using a given [vec3](../../../../api/library/math/cs/vec3_cs.md) vector as a source.
### Arguments

- *int* **column** - Column index.
- *vec3* **v** - Source vector.

## vec3 GetColumn ( int column )

Returns the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

Return value.
## float Get ( int row , int column )

Returns the matrix element specified by a given row and column.
### Arguments

- *int* **row** - Row index.
- *int* **column** - Column index.

### Return value

Resulting *float* value.
## float Set ( int row , int column , float v )

Sets the value using the specified argument(s).
### Arguments

- *int* **row** - Row index.
- *int* **column** - Column index.
- *float* **v** - A *float* value to be used.

### Return value

Resulting *float* value.
## void Clear ( )

Clears the value by setting all components/elements to 0.
## void SetZero ( )

Sets all matrix elements equal to **0**.
## void SetIdentity ( )

Sets the matrix equal to the identity matrix.
## void SetSkewSymmetric ( vec3 v )


Fills the skew-symmetric matrix using a given [vec3](../../../../api/library/math/cs/vec3_cs.md) source vector.


```text
Skew-symmetric matrix:
    | 0.0f   	-v.z	   v.y |
S=  | v.z       0.0f      -v.x |
    | -v.y      v.x       0.0f |

```


### Arguments

- *vec3* **v** - Source vector.

## void SetRotate ( vec3 axis , float angle )

Sets the rotation matrix for a given axis.
### Arguments

- *vec3* **axis** - Axis of rotation.
- *float* **angle** - Angle, in degrees.

## void SetRotateX ( float angle )

Sets X rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## void SetRotateY ( float angle )

Sets Y rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## void SetRotateZ ( float angle )

Sets Z rotation matrix.
### Arguments

- *float* **angle** - Angle, in degrees.

## void SetScale ( vec3 v )


Fills the scaling matrix using a given [vec3](../../../../api/library/math/cs/vec3_cs.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f	  0.0f |
S=  | 0.0f      v.y    	  0.0f |
    | 0.0f      0.0f      v.z  |

```


### Arguments

- *vec3* **v** - Source vector.

## string ToString ( )

Converts the current value to a *string* value.
### Return value

Resulting *string* value.
