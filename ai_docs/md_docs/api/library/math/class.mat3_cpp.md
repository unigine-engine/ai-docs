# Unigine::Math::mat3 Struct (CPP)

**Header:** #include <UnigineMathLibMat3.h>


This class represents a matrix of nine (3x3) float components.


## mat3 Struct

### Members

---

## mat3 ( )

Default constructor. Produces an identity matrix.
## mat3 ( float v )


Constructor. Initializes the matrix using a given scalar value.


```cpp
mat3(2.0);

/* Creates a matrix
| 2.0 	2.0		2.0	|
| 2.0 	2.0		2.0	|
| 2.0 	2.0		2.0	|
*/

```


### Arguments

- *float* **v** - Scalar value.

## mat3 ( const mat3& m )

Constructor. Initializes the matrix by copying a given source matrix.
### Arguments

- *const mat3&* **m** - Source matrix.

## mat3 ( const mat2& m )


Constructor. Initializes the matrix using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01	  0.0f |
M=  | m10    m11      0.0f |
    | 0.0f   0.0f     1.0f |

```


### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## mat3 ( const mat4& m )

Constructor. Initializes the matrix using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## mat3 ( const dmat4& m )

Constructor. Initializes the matrix using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## mat3 ( const vec3& c0 , const vec3& c1 , const vec3& c2 )


Constructor. Initializes the matrix using given three [vec3](../../../api/library/math/class.vec3_cpp.md) vectors.


```text
Resulting matrix:
    | col0.x  	 col1.x	  	col2.x |
M=  | col0.y   	 col1.y     col2.y |
    | col0.z   	 col1.z     col2.z |

```


### Arguments

- *const vec3&* **c0** - Source vector for the first column.
- *const vec3&* **c1** - Source vector for the second column
- *const vec3&* **c2** - Source vector for the third column

## mat3 ( const quat& q )


Constructor. Initializes the matrix using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).


```text
For the quaternion (x, y, z, w) the corresponding rotation matrix M is defined as follows:
    | 1 - 2y� - 2z�    2xy + 2wz      	2xz - 2wy     |
M=  | 2xy - 2wz        1 - 2x� - 2z�    2yz + 2wx     |
    | 2xz + 2wy        2yz - 2wx        1 - 2x� - 2y� |

```


### Arguments

- *const quat&* **q** - Source quaternion.

## mat3 ( float v , ConstexprTag )


Constructor. Initializes the matrix using a given constant float value.


```text
Resulting matrix:
    | v   v   v |
M=  | v   v   v |
    | v   v   v |

```


### Arguments

- *float* **v** - Value.
- *ConstexprTag*  - Auxiliary tag.

## mat3 ( float m00_ , float m10_ , float m20_ , float m01_ , float m11_ , float m21_ , float m02_ , float m12_ , float m22_ , ConstexprTag )


Constructor. Initializes the matrix with given constant float values.


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
- *ConstexprTag*  - Auxiliary tag.

## mat3 ( const mat3x3_values& m )

Constructor. Initializes the matrix using a given source matrix values.
### Arguments

- *[const mat3x3_values&](/api/library/math/auxiliary_types#mat3x3_values)* **m** - The source value storing matrix float values.

## void set ( int row , int column , float v )

Sets a new value of the matrix element specified by row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.
- *float* **v** - The value to be set.

## void set ( const dmat4& m )

Sets the matrix using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). The matrix elements are set equal to corresponding elements of the source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## void set ( const mat4& m )

Sets the matrix using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4). The matrix elements are set equal to corresponding elements of the source matrix.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## void set ( const mat3x3_values& m )

Sets the matrix using the argument float values.
### Arguments

- *[const mat3x3_values&](/api/library/math/auxiliary_types#mat3x3_values)* **m** - The source value storing matrix float values.

## void set ( const quat& q )


Sets the matrix using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).


```text
For the quaternion (x, y, z, w) the corresponding rotation matrix M is defined as follows:
    | 1 - 2y� - 2z�    2xy + 2wz      	2xz - 2wy     |
M=  | 2xy - 2wz        1 - 2x� - 2z�    2yz + 2wx     |
    | 2xz + 2wy        2yz - 2wx        1 - 2x� - 2y� |

```


### Arguments

- *const quat&* **q** - Source quaternion.

## void set ( const mat3& m )

Sets the matrix equal to the specified source matrix.
### Arguments

- *const mat3&* **m** - Source matrix.

## void set ( const mat2& m )


Sets new matrix values using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01	  0.0f |
M=  | m10    m11      0.0f |
    | 0.0f   0.0f     1.0f |

```


### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## void get ( mat3x3_values& m ) const

Returns the matrix values by filling the specified argument.
### Arguments

- *[mat3x3_values&](/api/library/math/auxiliary_types#mat3x3_values)* **m** - The destination value to store matrix float values.

## mat4x3_values & get ( )

Returns the value storing matrix float values.
### Return value

The value storing matrix float values.
## const mat4x3_values & get ( ) const

Returns the constant value storing matrix float values.
### Return value

The constant value storing matrix float values.
## float & get ( int row , int column )

Returns the reference to the matrix element specified by a given row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.

### Return value

Matrix element reference.
## float get ( int row , int column ) const

Returns the value of the matrix element specified by given row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.

### Return value

Matrix element value.
## void setColumn ( int column , const vec3& v )

Sets the specified column of the matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) vector as a source.
### Arguments

- *int* **column** - Column.
- *const vec3&* **v** - Source vector.

## vec3 getColumn ( int column ) const

Returns the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [vec3](../../../api/library/math/class.vec3_cpp.md) vector with column values.
## void setDiagonal ( const vec3& v )

Sets the main diagonal of the matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) vector as a source.
### Arguments

- *const vec3&* **v** - Source vector.

## vec3 getDiagonal ( ) const

Returns the main diagonal of the matrix.
### Return value

The [vec3](../../../api/library/math/class.vec3_cpp.md) vector with the elements of the main diagonal.
## void setIdentity ( )

Sets the matrix equal to the identity matrix.
## quat getQuat ( ) const

Returns the [quaternion](../../../api/library/math/class.quat_cpp.md) of the matrix values.
### Return value

Quaternion.
## void setRotate ( const vec3& axis , float angle )

Sets the rotation matrix for a given axis.
### Arguments

- *const vec3&* **axis** - Rotation axis.
- *float* **angle** - Rotation angle, in degrees.

## void setRotateX ( float angle )

Sets X rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRotateY ( float angle )

Sets Y rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRotateZ ( float angle )

Sets Z rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRow ( int row , const vec3& v )

Sets the specified row of the matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) vector as a source.
### Arguments

- *int* **row** - Row.
- *const vec3&* **v** - Source vector.

## vec3 getRow ( int row ) const

Returns the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [vec3](../../../api/library/math/class.vec3_cpp.md) vector with column values.
## void setScale ( const vec3& v )


Fills the scaling matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f	  0.0f |
S=  | 0.0f      v.y    	  0.0f |
    | 0.0f      0.0f      v.z  |

```


### Arguments

- *const vec3&* **v** - Source vector.

## void setSkewSymmetric ( const vec3& v )


Fills the skew-symmetric matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.


```text
Skew-symmetric matrix:
    | 0.0f   	-v.z	   v.y |
S=  | v.z       0.0f      -v.x |
    | -v.y      v.x       0.0f |

```


### Arguments

- *const vec3&* **v** - Source vector.

## void setZero ( )

Sets all matrix elements equal to **0**.
## const float * operator const float * ( ) const

Performs type conversion to const float *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## float * operator float * ( )

Performs type conversion to float *.
## void * operator void * ( )

Performs type conversion to void *.
## mat3 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting matrix.
## mat3 & operator*= ( const mat3& m )

Performs matrix multiplication.
### Arguments

- *const mat3&* **m** - Matrix.

### Return value

Resulting matrix.
## mat3 & operator+= ( const mat3& m )

Performs matrix addition.
### Arguments

- *const mat3&* **m** - Matrix.

### Return value

Resulting matrix.
## mat3 operator- ( ) const

Performs matrix negation.
### Return value

Resulting matrix.
## mat3 & operator-= ( const mat3& m )

Performs matrix subtraction.
### Arguments

- *const mat3&* **m** - mat3 matrix.

### Return value

Resulting matrix.
## mat3 & operator= ( const mat3& m )

Performs matrix assignment. Destination matrix = Source matrix.
### Arguments

- *const mat3&* **m** - Source matrix

### Return value

Result.
## float operator[] ( int i ) const

Performs array access to the matrix item using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item.
## float & operator[] ( int i )

Performs array access to the matrix item reference using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item reference.
## vec3 getAxisX ( ) const


Returns the normalized vector representing the X axis. Call this method to get the right or left vector of the matrix:


```cpp
matrix.getAxisX(); // the left vector
-matrix.getAxisX(); // the right vector

```


### Return value

Vector representing the X axis.
## vec3 getAxisY ( ) const


Returns the normalized vector representing the Y axis. Call this method to get the back or forward vector of the matrix:


```cpp
matrix.getAxisY(); // the back vector
-matrix.getAxisY(); // the forward vector

```


### Return value

Vector representing the Y axis.
## vec3 getAxisZ ( ) const


Returns the normalized vector representing the Z axis. Call this method to get the up or down vector of the matrix:


```cpp
matrix.getAxisZ(); // the up vector
-matrix.getAxisZ(); // the down vector

```


### Return value

Vector representing the Z axis.
## float trace ( ) const

Returns the trace of the matrix.
### Return value

Trace of the matrix.
## float determinant ( ) const

Returns the determinant of the matrix.
### Return value

Determinant of the matrix.
