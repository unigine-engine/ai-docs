# Unigine.mat2 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## mat2 Class

### Properties

## 🔒︎ float m00

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m10

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m01

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ float m11

The Matrix element in the corresponding row and column **mxy = M[x, y]**. Provides convenient access to matrix elements.
## 🔒︎ mat2 ZERO

The Matrix, filled with zeros (0).
## 🔒︎ mat2 ONE

The Matrix, filled with ones (1).
## 🔒︎ mat2 IDENTITY

The Identity matrix.
## 🔒︎ vec2 Row0

The First row.
## 🔒︎ vec2 Row1

The Second row.
## 🔒︎ vec2 Column0

The First column.
## 🔒︎ vec2 Column1

The Second column.
## 🔒︎ vec2 AxisX

The X axis.
## 🔒︎ vec2 AxisY

The Y axis.
## 🔒︎ vec2 Diagonal

The Vector containing diagonal elements of the matrix.
## 🔒︎ float Trace

The Trace of the matrix: (sum of its diagonal elements).
## 🔒︎ float Determinant

The Determinant of the matrix.
### Members

---

## bool operator== ( mat2 v0 , mat2 v1 )

Performs equal comparison.
### Arguments

- *mat2* **v0** - First value.
- *mat2* **v1** - Second value.

## bool operator!= ( mat2 v0 , mat2 v1 )

Not equal comparison.
### Arguments

- *mat2* **v0** - First value.
- *mat2* **v1** - Second value.

## bool Equals ( mat2 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *mat2* **other** - Value to be checked for equality.

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
## mat2 operator- ( mat2 m )

Subtraction.
### Arguments

- *mat2* **m** - Matrix.

## mat2 operator* ( mat2 m , float v )

Multiplication.
### Arguments

- *mat2* **m** - Matrix.
- *float* **v** - Value.

## vec2 operator* ( mat2 m , vec2 v )

Multiplication.
### Arguments

- *mat2* **m** - Matrix.
- *vec2* **v** - Value.

## vec2 operator* ( vec2 v , mat2 m )

Multiplication.
### Arguments

- *vec2* **v** - Value.
- *mat2* **m** - Matrix.

## dvec2 operator* ( mat2 m , dvec2 v )

Multiplication.
### Arguments

- *mat2* **m** - Matrix.
- *dvec2* **v** - Value.

## dvec2 operator* ( dvec2 v , mat2 m )

Multiplication.
### Arguments

- *dvec2* **v** - Value.
- *mat2* **m** - Matrix.

## mat2 operator* ( mat2 m0 , mat2 m1 )

Matrices multiplication.
### Arguments

- *mat2* **m0** - First matrix.
- *mat2* **m1** - Second matrix.

### Return value

Result matrix.
## mat2 operator+ ( mat2 m0 , mat2 m1 )

Matrices addition.
### Arguments

- *mat2* **m0** - First matrix.
- *mat2* **m1** - Second matrix.

## mat2 operator- ( mat2 m0 , mat2 m1 )

Matrices subtraction.
### Arguments

- *mat2* **m0** - First matrix.
- *mat2* **m1** - Second matrix.

## void Set ( float m00_ , float m10_ , float m01_ , float m11_ )

Sets the value using the specified argument(s).
### Arguments

- *float* **m00_** - m00_ element.
- *float* **m10_** - m10_ element.
- *float* **m01_** - m01_ element.
- *float* **m11_** - m11_ element.

## void Set ( float v )

Sets the value using the specified argument(s).
### Arguments

- *float* **v** - A *float* value to be used.

## void Set ( float[] m )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **m** - Source matrix.

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

## void Set ( vec2 col0 , vec2 col1 )

Sets the value using the specified argument(s).
### Arguments

- *vec2* **col0** - First column.
- *vec2* **col1** - Second column.

## void SetRow ( int row , vec2 v )

Sets the specified row of the matrix using a given [vec2](../../../../api/library/math/cs/vec2_cs.md) vector as a source.
### Arguments

- *int* **row** - Row index.
- *vec2* **v** - Source vector.

## vec2 GetRow ( int row )

Returns the specified matrix row.
### Arguments

- *int* **row** - Row index.

### Return value

Return value.
## void SetColumn ( int column , vec2 v )

Sets the specified column of the matrix using a given [vec2](../../../../api/library/math/cs/vec2_cs.md) vector as a source.
### Arguments

- *int* **column** - Column index.
- *vec2* **v** - Source vector.

## vec2 GetColumn ( int column )

Returns the specified matrix column.
### Arguments

- *int* **column** - Column index.

### Return value

Return value.
## float Get ( int row , int column )

Returns the matrix element specified by given row and column.
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
## void SetRotate ( float angle )


Fills the rotation matrix using a given angle.


```text
Rotation matrix:
    | cos(angle)   	-sin(angle) |
R=  | sin(angle)     cos(angle) |

```


### Arguments

- *float* **angle** - Angle, in degrees.

## void SetScale ( vec2 v )


Fills the scaling matrix using a given [vec2](../../../../api/library/math/cs/vec2_cs.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f |
S=  | 0.0f      v.y  |

```


### Arguments

- *vec2* **v** - Source vector.

## string ToString ( )

Converts the current value to a *string* value.
### Return value

Resulting *string* value.
