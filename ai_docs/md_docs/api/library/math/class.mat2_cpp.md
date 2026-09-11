# Unigine::Math::mat2 Struct (CPP)

**Header:** #include <UnigineMathLibMat2.h>


This class represents a matrix of four (2x2) float components.


## mat2 Struct

### Members

---

## mat2 ( )

Default constructor. Produces an identity matrix.
## mat2 ( const mat2& m )

Constructor. Initializes the matrix by copying a given source matrix.
### Arguments

- *const mat2&* **m** - Source matrix.

## mat2 ( float v )


Constructor. Initializes the matrix using a given scalar value.


```cpp
mat2(2.0);

/* Creates a matrix
| 2.0	2.0	|
| 2.0	2.0	|
*/

```


### Arguments

- *float* **v** - Scalar value.

## mat2 ( const mat3& m )

Constructor. Initializes the matrix using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## mat2 ( const mat4& m )

Constructor. Initializes the matrix using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## mat2 ( const dmat4& m )

Constructor. Initializes the matrix using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## mat2 ( const vec2& col0 , const vec2& col1 )


Constructor. Initializes the matrix by given two [vec2](../../../api/library/math/class.vec2_cpp.md) vectors.


```text
Resulting matrix:
    | col0.x   	 col1.x |
M=  | col0.y     col1.y |

```


### Arguments

- *const vec2&* **col0** - Source vector for the first column.
- *const vec2&* **col1** - Source vector for the second column.

## mat2 ( float m00_ , float m10_ , float m01_ , float m11_ )


Constructor. Initializes the matrix with given float values.


```text
Resulting matrix:
    | m00_   m10_ |
M=  | m01_   m11_ |

```


### Arguments

- *float* **m00_** - m00_ element.
- *float* **m10_** - m10_ element.
- *float* **m01_** - m01_ element.
- *float* **m11_** - m11_ element.

## mat2 ( float m00_ , float m10_ , float m01_ , float m11_ , ConstexprTag )


Constructor. Initializes the matrix with given constant float values.


```text
Resulting matrix:
    | m00_   m10_ |
M=  | m01_   m11_ |

```


### Arguments

- *float* **m00_** - m00_ element.
- *float* **m10_** - m10_ element.
- *float* **m01_** - m01_ element.
- *float* **m11_** - m11_ element.
- *ConstexprTag*  - Auxiliary tag.

## mat2 ( float v , ConstexprTag )


Constructor. Initializes the matrix with the given float value.


```text
Resulting matrix:
    | v   v |
M=  | v   v |

```


### Arguments

- *float* **v** - Value.
- *ConstexprTag*  - Auxiliary tag.

## mat2 ( const mat2x2_values& m )

Constructor. Initializes the matrix using a given source matrix values.
### Arguments

- *[const mat2x2_values&](/api/library/math/auxiliary_types#mat2x2_values)* **m** - The source value storing matrix float values.

## void set ( const mat2x2_values& m )

Sets the matrix using the argument float values.
### Arguments

- *[const mat2x2_values&](/api/library/math/auxiliary_types#mat2x2_values)* **m** - The source value storing matrix float values.

## void set ( const mat2& m )

Sets the matrix equal to the specified source matrix.
### Arguments

- *const mat2&* **m** - Source matrix.

## void set ( const mat3& m )

Sets the matrix using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). Values **m00**, **m01**, **m10**, **m11** from the source matrix are used.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## void set ( const mat4& m )

Sets the matrix using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4). Values **m00**, **m01**, **m10**, **m11** from the source matrix are used.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## void set ( const dmat4& m )

Sets the matrix using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4). Values **m00**, **m01**, **m10**, **m11** from the source matrix are used.
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## void set ( int row , int column , float v )

Sets a new value of the matrix element specified by row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.
- *float* **v** - The value to be set.

## void get ( mat2x2_values& m ) const

Returns the matrix values by filling the specified argument.
### Arguments

- *[mat2x2_values&](/api/library/math/auxiliary_types#mat2x2_values)* **m** - The destination value to store matrix float values.

## mat2x2_values & get ( )

Returns the value storing matrix float values.
### Return value

The value storing matrix float values.
## const mat2x2_values & get ( ) const

Returns the constant value storing matrix float values.
### Return value

The constant value storing matrix float values.
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
## void setColumn ( int column , const vec2& v )

Sets the specified column of the matrix using a given [vec2](../../../api/library/math/class.vec2_cpp.md) vector as a source.
### Arguments

- *int* **column** - Column.
- *const vec2&* **v** - Source vector.

## vec2 getColumn ( int column ) const

Returns the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [vec2](../../../api/library/math/class.vec2_cpp.md) vector with column values.
## void setIdentity ( )

Sets the matrix equal to the identity matrix.
## void setRotate ( float angle )


Fills the rotation matrix using a given angle.


```text
Rotation matrix:
    | cos(angle)   	-sin(angle) |
R=  | sin(angle)     cos(angle) |

```


### Arguments

- *float* **angle** - Rotation angle, in degrees.

## void setRow ( int row , const vec2& v )

Sets the specified row of the matrix using a given [vec2](../../../api/library/math/class.vec2_cpp.md) vector as a source.
### Arguments

- *int* **row** - Row.
- *const vec2&* **v** - Source vector.

## vec2 getRow ( int row ) const

Returns the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [vec2](../../../api/library/math/class.vec2_cpp.md) vector with row values.
## void setScale ( const vec2& v )


Fills the scaling matrix using a given [vec2](../../../api/library/math/class.vec2_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f |
S=  | 0.0f      v.y  |

```


### Arguments

- *const vec2&* **v** - Source vector.

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
## mat2 & operator*= ( const mat2& m )

Performs matrix multiplication.
### Arguments

- *const mat2&* **m** - Matrix.

### Return value

Resulting matrix.
## mat2 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting matrix.
## mat2 & operator+= ( const mat2& m )

Performs matrix addition.
### Arguments

- *const mat2&* **m** - Matrix.

### Return value

Resulting matrix.
## mat2 operator- ( ) const

Performs matrix negation.
### Return value

Resulting matrix.
## mat2 & operator-= ( const mat2& m )

Performs matrix subtraction.
### Arguments

- *const mat2&* **m** - Matrix.

### Return value

Resulting matrix.
## mat2 & operator= ( const mat2& m )

Performs matrix assignment. Destination matrix = Source matrix.
### Arguments

- *const mat2&* **m** - Source matrix.

### Return value

Result.
## float operator[] ( int i ) const

Performs array access to the matrix item using a given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item.
## float & operator[] ( int i )

Performs array access to the matrix item reference using a given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item reference.
## float trace ( ) const

Returns the trace of the matrix.
### Return value

Trace of the matrix.
## float determinant ( ) const

Returns the determinant of the matrix.
### Return value

Determinant of the matrix.
