# Unigine::Math::mat4 Struct (CPP)

**Header:** #include <UnigineMathLibMat4.h>


This class represents a matrix of sixteen (4x4) float components.


## mat4 Struct

### Members

---

## mat4 ( )

Default constructor. Produces an identity matrix.
## mat4 ( float v )


Constructor. Initializes the matrix using a given scalar value.


```cpp
mat4(2.0);

/* Creates a matrix
| 2.0 	2.0 	2.0		2.0	|
| 2.0 	2.0 	2.0		2.0	|
| 2.0 	2.0 	2.0		2.0	|
| 2.0 	2.0 	2.0		2.0	|
*/

```


### Arguments

- *float* **v** - Scalar value.

## mat4 ( const mat3& m )


Constructor. Initializes the matrix using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 m02	  0.0f |
M=  | m10    m11  	 m12      0.0f |
    | m20    m21     m22      0.0f |
    | 0.0f   0.0f    0.0f     1.0f |

```


### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## mat4 ( const mat4& m )

Constructor. Initializes the matrix by copying a given source matrix.
### Arguments

- *const mat4&* **m** - Source matrix.

## explicit mat4 ( const dmat4& m )

Constructor. Initializes the matrix using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## mat4 ( const vec4& c0 , const vec4& c1 , const vec4& c2 , const vec4& c3 )


Constructor. Initializes the matrix using given three [vec4](../../../api/library/math/class.vec4_cpp.md) vectors.


```text
Resulting matrix:
    | col0.x  	 col1.x	  	col2.x	   col3.x |
M=  | col0.y   	 col1.y	  	col2.y     col3.y |
    | col0.z   	 col1.z	  	col2.z     col3.z |
	| col0.w   	 col1.w	  	col2.w     col3.w |

```


### Arguments

- *const vec4&* **c0** - Source vector for the first column.
- *const vec4&* **c1** - Source vector for the second column.
- *const vec4&* **c2** - Source vector for the third column.
- *const vec4&* **c3** - Source vector for the fourth column.

## explicit mat4 ( const quat& q )


Constructor. Initializes the matrix using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).


```text
For the quaternion (x, y, z, w) the corresponding rotation matrix M is defined as follows:
    | 1 - 2y� - 2z�    2xy + 2wz      	2xz - 2wy     	0.0f |
M=  | 2xy - 2wz        1 - 2x� - 2z�    2yz + 2wx     	0.0f |
    | 2xz + 2wy        2yz - 2wx        1 - 2x� - 2y� 	0.0f |
    |  0.0f            0.0f        		0.0f 			1.0f |

```


### Arguments

- *const quat&* **q** - Source quaternion.

## mat4 ( const mat3& m , const vec3& v )

Constructor. Initializes the matrix using a given source [mat3](../../../api/library/math/class.mat3_cpp.md) matrix (3x3) and a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).
- *const vec3&* **v** - Source vector.

## mat4 ( const quat& q , const vec3& v )

Constructor. Initializes the matrix using a given [quaternion](../../../api/library/math/class.quat_cpp.md) and a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const quat&* **q** - Source quaternion.
- *const vec3&* **v** - Source vector.

## mat4 ( const mat2& m )


Constructor. Initializes the matrix using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 0.0f	  0.0f |
M=  | m10    m11  	 0.0f     0.0f |
    | 0.0f   0.0f    1.0f     0.0f |
    | 0.0f   0.0f    0.0f     1.0f |

```


### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## mat4 ( float m00_ , float m10_ , float m20_ , float m30_ , float m01_ , float m11_ , float m21_ , float m31_ , float m02_ , float m12_ , float m22_ , float m32_ , float m03_ , float m13_ , float m23_ , float m33_ )


Constructor. Initializes the matrix using a given float values.


```text
Resulting matrix:
    | m00_  m01_  	m02_	 m03_ |
M=  | m10_  m11_  	m12_     m13_ |
    | m20_  m21_    m22_     m23_ |
    | m30_  m31_    m32_     m33_ |

```


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

## mat4 ( float m00_ , float m10_ , float m20_ , float m30_ , float m01_ , float m11_ , float m21_ , float m31_ , float m02_ , float m12_ , float m22_ , float m32_ , float m03_ , float m13_ , float m23_ , float m33_ , ConstexprTag )


Constructor. Initializes the matrix using a given constant float values.


```text
Resulting matrix:
    | m00_  m01_  	m02_	 m03_ |
M=  | m10_  m11_  	m12_     m13_ |
    | m20_  m21_    m22_     m23_ |
    | m30_  m31_    m32_     m33_ |

```


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
- *ConstexprTag*  - Auxiliary tag.

## mat4 ( float v , ConstexprTag )


Constructor. Initializes the matrix using a given constant float value.


```text
Resulting matrix:
    | v   v   v   v|
M=  | v   v   v   v|
    | v   v   v   v|
    | v   v   v   v|

```


### Arguments

- *float* **v** - Value.
- *ConstexprTag*  - Auxiliary tag.

## mat4 ( const mat4x4_values& m )

Constructor. Initializes the matrix using the given source matrix values.
### Arguments

- *[const mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The source value storing matrix float values.

## mat4 ( const mat4x4_values& m , int transposed )

Constructor. Initializes the matrix using the given source matrix values.
### Arguments

- *[const mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## mat4 ( const dmat4x4_values& m )

Constructor. Initializes the matrix with float values using the given source matrix double values.
### Arguments

- *[const dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The source value storing matrix double values.

## mat4 ( const dmat4x4_values& m , int transpose )

Constructor. Initializes the matrix with float values using the given source matrix double values.
### Arguments

- *[const dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The source value storing matrix double values.
- *int* **transpose** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const mat4x4_values& m , int transposed )

Sets the matrix using the argument float values.
### Arguments

- *[const mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const dmat4x4_values& m , int transpose )

Sets the matrix with float values using the argument with double values.
### Arguments

- *[const dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The source value storing matrix double values.
- *int* **transpose** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const mat2& m )


Sets new matrix values using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 0.0f	  0.0f |
M=  | m10    m11  	 0.0f     0.0f |
    | 0.0f   0.0f    1.0f     0.0f |
    | 0.0f   0.0f    0.0f     1.0f |

```


### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## void set ( const mat3& m , const vec3& v )

Sets new matrix values using a given source [mat3](../../../api/library/math/class.mat3_cpp.md) matrix (3x3) and a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).
- *const vec3&* **v** - Source vector.

## void set ( const quat& q , const vec3& v )

Sets new matrix values using a given [quaternion](../../../api/library/math/class.quat_cpp.md) and a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const quat&* **q** - Source quaternion.
- *const vec3&* **v** - Source vector.

## void set ( const mat3& m )


Sets new matrix values using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 m02	  0.0f |
M=  | m10    m11  	 m12      0.0f |
    | m20    m21     m22      0.0f |
    | 0.0f   0.0f    0.0f     1.0f |

```


### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## void set ( const quat& q )

Sets new matrix values using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const quat&* **q** - Source quaternion.

## void set ( const mat4& m )

Sets the matrix equal to the specified source matrix.
### Arguments

- *const mat4&* **m** - Source matrix.

## void set ( const dmat4& m )

Sets new matrix values using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## void set ( int row , int column , float v )

Sets a new value of the matrix element specified by row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.
- *float* **v** - The value to be set.

## float & get ( int row , int column )

Returns the reference to the matrix element specified by given row and column.
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
## void get ( mat4x4_values& m , int transpose ) const

Returns the matrix values by filling the specified argument.
### Arguments

- *[mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The destination value to store matrix float values.
- *int* **transpose** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## mat4x4_values & get ( )

Returns the value storing matrix float values.
### Return value

The value storing matrix float values.
## const mat4x4_values & get ( ) const

Returns the constant value storing matrix float values.
### Return value

The constant value storing matrix float values.
## void setColumn ( int column , const vec4& v )

Sets the specified column of the matrix using a given [vec4](../../../api/library/math/class.vec4_cpp.md) vector as a source.
### Arguments

- *int* **column** - Column.
- *const vec4&* **v** - Source vector.

## vec4 getColumn ( int column ) const

Returns the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [vec4](../../../api/library/math/class.vec4_cpp.md) vector with column values.
## void setColumn3 ( int column , const vec3& v )

Sets the specified column of the matrix using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector as a source, the last element of the column remains as is.
### Arguments

- *int* **column** - Column.
- *const vec3&* **v** - Three-component source vector.

## vec3 getColumn3 ( int column ) const

Returns the XYZ components of the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [vec3](../../../api/library/math/class.vec3_cpp.md) vector with the first three elements of the specified matrix column.
## void setDiagonal ( const vec4& v )

Sets the main diagonal of the matrix using a given [vec4](../../../api/library/math/class.vec4_cpp.md) vector as a source.
### Arguments

- *const vec4&* **v** - Source vector.

## vec4 getDiagonal ( ) const

Returns the main diagonal of the matrix.
### Return value

The [vec4](../../../api/library/math/class.vec4_cpp.md) vector with the element of the main diagonal.
## void setIdentity ( )

Sets the matrix equal to the identity matrix.
## void setRotate ( const vec3& axis , float angle )

Sets the rotation matrix for a given axis.
### Arguments

- *const vec3&* **axis** - Rotation axis.
- *float* **angle** - Rotation angle, in degrees.

## quat getRotate ( ) const

Returns the [quaternion](../../../api/library/math/class.quat_cpp.md), representing the rotation part of the matrix.
### Return value

Matrix rotation part.
## void setRotateX ( float angle )

Sets X rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRotateY ( float angle )

Sets Y rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRotateZ ( float angle )

Set Z rotation matrix.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRow ( int row , const vec4& v )

Sets the specified row of the matrix using a given [vec4](../../../api/library/math/class.vec4_cpp.md) vector as a source.
### Arguments

- *int* **row** - Row.
- *const vec4&* **v** - Source vector.

## vec4 getRow ( int row ) const

Returns the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [vec4](../../../api/library/math/class.vec4_cpp.md) vector with row values.
## void setRow3 ( int row , const vec3& v )

Sets the specified row of the matrix using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector as a source, the last element of the row remains as is.
### Arguments

- *int* **row** - Row.
- *const vec3&* **v** - Three-component source vector.

## vec3 getRow3 ( int row ) const

Returns the first three elements of the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [vec3](../../../api/library/math/class.vec3_cpp.md) vector with the first three elements of the specified matrix row.
## void setScale ( const vec3& v )


Fills the scaling matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f  	  0.0f	    0.0f |
S=  | 0.0f      v.y  	  0.0f      0.0f |
    | 0.0f      0.0f      v.z  		0.0f |
    | 0.0f      0.0f      0.0f  	1.0f |

```


### Arguments

- *const vec3&* **v** - Source vector.

## vec3 getScale ( ) const

Returns the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector, representing the scaling part of the matrix.
### Return value

Three-component vector with the scaling part of the matrix.
## void setTranslate ( const vec3& v )


Fills the translation matrix using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |
    | 0.0f      0.0f      0.0f     1.0f |

```


### Arguments

- *const vec3&* **v** - Source vector.

## vec3 getTranslate ( ) const

Returns the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector, representing the translation part of the matrix.
### Return value

Three-component vector with the translation part of the matrix.
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
## mat4 & operator*= ( const mat4& m )

Performs matrix multiplication.
### Arguments

- *const mat4&* **m** - Matrix.

### Return value

Resulting matrix.
## mat4 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting matrix.
## mat4 & operator+= ( const mat4& m )

Performs matrix addition.
### Arguments

- *const mat4&* **m** - Matrix.

### Return value

Resulting matrix.
## mat4 operator- ( ) const

Performs matrix negation.
## mat4 & operator-= ( const mat4& m )

Performs matrix subtraction.
### Arguments

- *const mat4&* **m** - Matrix.

### Return value

Resulting matrix.
## mat4 & operator= ( const mat4& m )

Performs matrix assignment. Destination matrix = Source matrix.
### Arguments

- *const mat4&* **m** - Source matrix.

### Return value

Result.
## float & operator[] ( int i )

Performs array access to the matrix item reference using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item reference.
## float operator[] ( int i ) const

Performs array access to the matrix item using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item.
## vec3 getAxisX ( ) const

Returns the normalized vector representing the X axis.
### Return value

Vector representing the X axis.
## vec3 getAxisY ( ) const

Returns the normalized vector representing the Y axis.
### Return value

Vector representing the Y axis.
## vec3 getAxisZ ( ) const

Returns the normalized vector representing the Z axis.
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
## float determinant3 ( ) const

Returns the determinant of the smaller 3x3 matrix of the original matrix.
### Return value

Determinant of the smaller 3x3 matrix.
