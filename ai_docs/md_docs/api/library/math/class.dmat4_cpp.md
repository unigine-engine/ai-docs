# Unigine::Math::dmat4 Struct (CPP)

**Header:** #include <UnigineMathLibDMat4.h>


This class represents a matrix of **twelve (3x4)** double components.


The *dmat4* matrix is used for world transformations only (translation, scaling, rotation). This matrix isn't used for 3D projection, so its last row is skipped (that's why its size is 3x4 not 4x4). It allows avoiding high memory usage and performance loss when using the double precision coordinates.


The first, the second and the third columns of the matrix represent the rotation and the scale of the origin. The last column contains the translation of the origin relatively to the world origin.


![](dmat4_matrix.png)


For any other purposes, the [mat4](../../../api/library/math/class.mat4_cpp.md) matrix can be used.


## dmat4 Struct

### Members

---

## dmat4 ( )

Default constructor. Produces an identity matrix.
## dmat4 ( const dvec3& c0 , const dvec3& c1 , const dvec3& c2 , const dvec3& c3 )


Constructor. Initializes the matrix using given three [dvec3](../../../api/library/math/class.dvec3_cpp.md) vectors.


```text
Resulting matrix:
    | col0.x  	 col1.x	  	col2.x	   col3.x |
M=  | col0.y   	 col1.y	  	col2.y     col3.y |
    | col0.z   	 col1.z	  	col2.z     col3.z |

```


### Arguments

- *const dvec3&* **c0** - Source vector for the first column.
- *const dvec3&* **c1** - Source vector for the second column.
- *const dvec3&* **c2** - Source vector for the third column.
- *const dvec3&* **c3** - Source vector for the fourth column.

## dmat4 ( const quat& q , const dvec3& v )

Constructor. Initializes the matrix using a given [quaternion](../../../api/library/math/class.quat_cpp.md) and a [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector.
### Arguments

- *const quat&* **q** - Source quaternion.
- *const dvec3&* **v** - Source vector.

## dmat4 ( const mat3& m , const dvec3& v )

Constructor. Initializes the matrix using a given source [mat3](../../../api/library/math/class.mat3_cpp.md) matrix (3x3) and a [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).
- *const dvec3&* **v** - Source vector.

## dmat4 ( const mat3& m )


Constructor. Initializes the matrix using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 m02	  0.0f |
M=  | m10    m11  	 m12      0.0f |
    | m20    m21     m22      0.0f |

```


### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## dmat4 ( const mat2& m )


Constructor. Initializes the matrix using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.


```text
Resulting matrix:
    | m00  	 m01  	 0.0f	  0.0f |
M=  | m10    m11  	 0.0f     0.0f |
    | 0.0f   0.0f    1.0f     0.0f |

```


### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## dmat4 ( double v )


Constructor. Initializes the matrix using a given scalar value.


```cpp
dmat4(2.0);

/* Creates a matrix
| 2.0 	2.0 	2.0		2.0	|
| 2.0 	2.0 	2.0		2.0	|
| 2.0 	2.0 	2.0		2.0	|
*/

```


### Arguments

- *double* **v** - Scalar value.

## dmat4 ( const dmat4& m )

Constructor. Initializes the matrix by copying a given source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix.

## explicit dmat4 ( const mat4& m )

Constructor. Initializes the matrix using a given source [mat4](../../../api/library/math/class.mat4_cpp.md) matrix (4x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## explicit dmat4 ( const quat& q )

Constructor. Initializes the matrix using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const quat&* **q** - Source quaternion.

## dmat4 ( const dmat4x4_values& m , int transposed )

Constructor. Initializes the matrix using the given source matrix values.
### Arguments

- *[const dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The source value storing matrix double values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## dmat4 ( const mat4x4_values& m , int transposed )

Constructor. Initializes the matrix using the given source matrix values.
### Arguments

- *[const mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## dmat4 ( const dmat4x3_values& m , int transposed )

Constructor. Initializes the matrix using the given source matrix values.
### Arguments

- *[const dmat4x3_values&](/api/library/math/auxiliary_types#dmat4x3_values)* **m** - The source value storing matrix double values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## dmat4 ( const mat4x3_values& m , int transposed )

Constructor. Initializes the matrix with double values using the given source matrix float values.
### Arguments

- *[const mat4x3_values&](/api/library/math/auxiliary_types#mat4x3_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## dmat4 ( double m00_ , double m10_ , double m20_ , double m01_ , double m11_ , double m21_ , double m02_ , double m12_ , double m22_ , double m03_ , double m13_ , double m23_ )


Constructor. Initializes the matrix using given double elements.


```text
 Resulting matrix:
    | m00  	 m01  	 m02	 m03 |
M=  | m10    m11  	 m12     m13 |
    | m20    m21     m22     m23 |

```


### Arguments

- *double* **m00_** - 00 element.
- *double* **m10_** - 10 element.
- *double* **m20_** - 20 element.
- *double* **m01_** - 01 element.
- *double* **m11_** - 11 element.
- *double* **m21_** - 21 element.
- *double* **m02_** - 02 element.
- *double* **m12_** - 12 element.
- *double* **m22_** - 22 element.
- *double* **m03_** - 03 element.
- *double* **m13_** - 13 element.
- *double* **m23_** - 23 element.

## dmat4 ( double v , ConstexprTag )


Constructor. Initializes every element of the matrix with the given double element.


```text
 Resulting matrix:
    | v    v 	v   v |
M=  | v    v  	v   v |
    | v    v    v   v |

```


### Arguments

- *double* **v** - Element to pave the matrix with.
- *ConstexprTag*  - Auxiliary tag.

## dmat4 ( double m00_ , double m10_ , double m20_ , double m01_ , double m11_ , double m21_ , double m02_ , double m12_ , double m22_ , double m03_ , double m13_ , double m23_ , ConstexprTag )


Constructor. Initializes the matrix using given double elements.


```text
 Resulting matrix:
    | m00  	 m01  	 m02	 m03 |
M=  | m10    m11  	 m12     m13 |
    | m20    m21     m22     m23 |

```


### Arguments

- *double* **m00_** - 00 element.
- *double* **m10_** - 10 element.
- *double* **m20_** - 20 element.
- *double* **m01_** - 01 element.
- *double* **m11_** - 11 element.
- *double* **m21_** - 21 element.
- *double* **m02_** - 02 element.
- *double* **m12_** - 12 element.
- *double* **m22_** - 22 element.
- *double* **m03_** - 03 element.
- *double* **m13_** - 13 element.
- *double* **m23_** - 23 element.
- *ConstexprTag*  - Auxiliary tag.

## void set ( int row , int column , double v )

Sets a new value of the matrix element specified by row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.
- *double* **v** - The value to be set.

## void set ( const mat4x4_values& m , int transposed )

Sets the matrix using the argument with float values.
### Arguments

- *[const mat4x4_values&](/api/library/math/auxiliary_types#mat4x4_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const dmat4x4_values& m , int transposed )

Sets the matrix with using the argument with double values.
### Arguments

- *[const dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The source value storing matrix double values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const mat4x3_values& m , int transposed )

Sets the matrix using the argument with float values.
### Arguments

- *[const mat4x3_values&](/api/library/math/auxiliary_types#mat4x3_values)* **m** - The source value storing matrix float values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const dmat4x3_values& m , int transposed )

Sets the matrix using the argument with double values.
### Arguments

- *[const dmat4x3_values&](/api/library/math/auxiliary_types#dmat4x3_values)* **m** - The source value storing matrix double values.
- *int* **transposed** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void set ( const mat2& m )

Sets new matrix values using a given [mat2](../../../api/library/math/class.mat2_cpp.md) source matrix (2x2). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat2&* **m** - Source matrix (2x2).

## void set ( const mat3& m )

Sets new matrix values using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## void set ( const quat& q , const dvec3& v )

Sets new matrix values using a given [quaternion](../../../api/library/math/class.quat_cpp.md) and a [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector.
### Arguments

- *const quat&* **q** - Source quaternion.
- *const dvec3&* **v** - Source vector.

## void set ( const quat& q )

Sets new matrix values using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const quat&* **q** - Source quaternion.

## void set ( const mat4& m )

Sets new matrix values using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4). The matrix elements are filled using corresponding elements of the source matrix.
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## void set ( const dmat4& m )

Sets the matrix equal to the specified source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix.

## void set ( const mat3& m , const dvec3& v )

Sets new matrix values using a given source [mat3](../../../api/library/math/class.mat3_cpp.md) matrix (3x3) and a [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector.
### Arguments

- *const mat3&* **m** - Source matrix (3x3).
- *const dvec3&* **v** - Source vector.

## double & get ( int row , int column )

Returns the reference to the matrix element specified by given row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.

### Return value

Matrix element reference.
## double get ( int row , int column ) const

Returns the value of the matrix element specified by given row and column.
### Arguments

- *int* **row** - Row.
- *int* **column** - Column.

### Return value

Matrix element value.
## void get ( dmat4x3_values& m , int transpose ) const

Returns the matrix values by filling the specified argument.
### Arguments

- *[dmat4x3_values&](/api/library/math/auxiliary_types#dmat4x3_values)* **m** - The destination value to store matrix double values.
- *int* **transpose** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## void get ( dmat4x4_values& m , int transpose ) const

Returns the matrix values by filling the specified argument.
### Arguments

- *[dmat4x4_values&](/api/library/math/auxiliary_types#dmat4x4_values)* **m** - The destination value to store matrix double values.
- *int* **transpose** - If set to **0** (by default), the matrix is specified in the column-major style; if set to 1, the matrix is transposed.

## dmat4x3_values & get ( )

Returns the value storing matrix double values.
### Return value

The value storing matrix double values.
## const dmat4x3_values & get ( ) const

Returns the constant value storing matrix double values.
### Return value

The constant value storing matrix double values.
## void setColumn ( int column , const dvec4& v )

Sets the specified column of the matrix using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector as a source.
### Arguments

- *int* **column** - Column.
- *const dvec4&* **v** - Source vector.

## dvec4 getColumn ( int column ) const

Returns the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [dvec4](../../../api/library/math/class.vec4_cpp.md) vector with column values.
## void setColumn3 ( int column , const dvec3& v )

Sets the specified column of the matrix using a given three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector as a source.
### Arguments

- *int* **column** - Column.
- *const dvec3&* **v** - Three-component source vector.

## dvec3 getColumn3 ( int column ) const

Returns the specified matrix column.
### Arguments

- *int* **column** - Column.

### Return value

The [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector with column values.
## void setIdentity ( )

Sets the matrix equal to the identity matrix.
## void setRotate ( const dvec3& axis , double angle )

Sets the rotation matrix for a given axis.
### Arguments

- *const dvec3&* **axis** - Rotation axis.
- *double* **angle** - Rotation angle, in degrees.

## quat getRotate ( ) const

Returns the [quaternion](../../../api/library/math/class.quat_cpp.md), representing the rotation part of the matrix.
### Return value

Matrix rotation part.
## void setRotateX ( double angle )

Sets X rotation matrix.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

## void setRotateY ( double angle )

Sets Y rotation matrix.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

## void setRotateZ ( double angle )

Sets Z rotation matrix.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

## void setRow ( int row , const dvec4& v )

Sets the specified row of the matrix using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector as a source.
### Arguments

- *int* **row** - Row.
- *const dvec4&* **v** - Source vector.

## dvec4 getRow ( int row ) const

Returns the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector with row values.
## void setRow3 ( int row , const dvec3& v )

Sets the specified row of the matrix using a given three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector as a source, the last element of the row remains as is.
### Arguments

- *int* **row** - Row.
- *const dvec3&* **v** - Three-component source vector.

## dvec3 getRow3 ( int row ) const

Returns the first three elements of the specified matrix row.
### Arguments

- *int* **row** - Row.

### Return value

The [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector with the first three elements of the specified matrix row.
## void setScale ( const dvec3& v )


Fills the scaling matrix using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f  	  0.0f	    0.0f |
S=  | 0.0f      v.y  	  0.0f      0.0f |
    | 0.0f      0.0f      v.z  		0.0f |

```


### Arguments

- *const dvec3&* **v** - Source vector.

## vec3 getScale ( ) const

Returns the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector, representing the scaling part of the matrix.
### Return value

Three-component vector with the scaling part of the matrix.
## void setTranslate ( const dvec3& v )


Fills the translation matrix using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |

```


### Arguments

- *const dvec3&* **v** - Source vector.

## dvec3 getTranslate ( ) const

Returns the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector, representing the translation part of the matrix.
### Return value

Three-component vector with the translation part of the matrix.
## void setZero ( )

Sets all matrix elements equal to **0**.
## const double * operator const double * ( ) const

Performs type conversion to const double *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## double * operator double * ( )

Performs type conversion to double *.
## void * operator void * ( )

Performs type conversion to void *.
## dmat4 & operator*= ( const dmat4& m )

Performs matrix multiplication.
### Arguments

- *const dmat4&* **m** - Matrix.

### Return value

Resulting matrix.
## dmat4 & operator*= ( double v )

Performs scalar multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting matrix.
## dmat4 & operator+= ( const dmat4& m )

Performs matrix addition.
### Arguments

- *const dmat4&* **m** - Matrix.

### Return value

Resulting matrix.
## dmat4 operator- ( ) const

Performs matrix negation.
### Return value

Resulting matrix.
## dmat4 & operator-= ( const dmat4& m )

Performs matrix subtraction.
### Arguments

- *const dmat4&* **m** - Matrix.

### Return value

Resulting matrix.
## dmat4 & operator= ( const dmat4& m )

Performs matrix assignment. Destination matrix = Source matrix.
### Arguments

- *const dmat4&* **m** - Source matrix.

### Return value

Result.
## double & operator[] ( int i )

Performs array access to the matrix item reference using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item reference.
## double operator[] ( int i ) const

Performs array access to the matrix item using given item index.
### Arguments

- *int* **i** - Matrix item index.

### Return value

Matrix item.
## dvec3 getAxisX ( ) const


Returns the normalized vector representing the X axis. Call this method to get the right or left vector of the matrix:


```cpp
matrix.getAxisX(); // the left vector
-matrix.getAxisX(); // the right vector

```


### Return value

Vector representing the X axis.
## dvec3 getAxisY ( ) const


Returns the normalized vector representing the Y axis. Call this method to get the back or forward vector of the matrix:


```cpp
matrix.getAxisY(); // the back vector
-matrix.getAxisY(); // the forward vector

```


### Return value

Vector representing the Y axis.
## dvec3 getAxisZ ( ) const


Returns the normalized vector representing the Z axis. Call this method to get the up or down vector of the matrix:


```cpp
matrix.getAxisZ(); // the up vector
-matrix.getAxisZ(); // the down vector

```


### Return value

Vector representing the Z axis.
## double determinant ( const dmat4& m )

Returns the determinant of the given matrix.
### Arguments

- *const dmat4&* **m** - Input matrix.

### Return value

Determinant of the matrix.
## dmat4 translate ( const dvec3& v )


Returns the translation matrix using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) translation vector.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |

```


### Arguments

- *const dvec3&* **v** - Translation vector.

### Return value

Translated matrix.
## dmat4 translate ( const dvec4& v )


Returns the translation matrix using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) translation vector.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |

```


### Arguments

- *const dvec4&* **v** - Translation vector.

### Return value

Translated matrix.
## dmat4 translate ( const dvec2& v )


Returns the translation matrix using a given [dvec2](../../../api/library/math/class.dvec2_cpp.md) translation vector.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |

```


### Arguments

- *const dvec2&* **v** - Translation vector.

### Return value

Translated matrix.
## dmat4 translate ( double x , double y , double z )


Returns the translation matrix using a [dvec3](../../../api/library/math/class.dvec3_cpp.md) translation vector with given components.


```text
Translation matrix:
    | 1.0f   	0.0f  	  0.0f	    v.x |
T=  | 0.0f      1.0f  	  0.0f      v.y |
    | 0.0f      0.0f      1.0f  	v.z |

```


### Arguments

- *double* **x** - X component of the translation vector.
- *double* **y** - Y component of the translation vector.
- *double* **z** - Z component of the translation vector.

### Return value

Translated matrix.
## dmat4 rotate ( const dvec3& axis , double angle )

Returns the rotation matrix for a given axis and an angle.
### Arguments

- *const dvec3&* **axis** - Rotation axis.
- *double* **angle** - Rotation angle, in degrees.

### Return value

Rotated matrix.
## dmat4 rotate ( double x , double y , double z , double angle )

Returns the rotation matrix for an angle and an axis with given components.
### Arguments

- *double* **x** - X component of the rotation vector.
- *double* **y** - Y component of the rotation vector.
- *double* **z** - Z component of the rotation vector.
- *double* **angle** - Rotation angle, in degrees.

### Return value

Rotated matrix.
## dmat4 rotateX ( double angle )

Returns the matrix rotated around the X-axis by a given angle.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

### Return value

Rotated matrix.
## dmat4 rotateY ( double angle )

Returns the matrix rotated around the Y-axis by a given angle.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

### Return value

Rotated matrix.
## dmat4 rotateZ ( double angle )

Returns the matrix rotated around the Z-axis by a given angle.
### Arguments

- *double* **angle** - Rotation angle, in degrees.

### Return value

Rotated matrix.
## dmat4 scale ( const dvec3& v )


Returns the matrix scaled by a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f  	  0.0f	    0.0f |
S=  | 0.0f      v.y  	  0.0f      0.0f |
    | 0.0f      0.0f      v.z  		0.0f |

```


### Arguments

- *const dvec3&* **v** - Source vector.

### Return value

Scaled matrix.
## dmat4 scale ( double x , double y , double z )


Returns the matrix scaled by a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.


```text
Scaling matrix:
    | v.x   	0.0f  	  0.0f	    0.0f |
S=  | 0.0f      v.y  	  0.0f      0.0f |
    | 0.0f      0.0f      v.z  		0.0f |

```


### Arguments

- *double* **x** - X component of the scale vector.
- *double* **y** - Y component of the scale vector.
- *double* **z** - Z component of the scale vector.

### Return value

Scaled matrix.
## dmat4 scale ( double x )


Returns the matrix scaled by a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector where every component is the same provided value.


```text
Scaling matrix:
    | v.x   	0.0f  	  0.0f	    0.0f |
S=  | 0.0f      v.y  	  0.0f      0.0f |
    | 0.0f      0.0f      v.z  		0.0f |

```


### Arguments

- *double* **x** - X, Y, and Z components of the scale vector.

### Return value

Scaled matrix.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
## dmat4 mul ( dmat4 & ret , const dmat4 & m , double v )

Matrix multiplication.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *double* **v** - The value of the scalar.

### Return value

The resulting matrix.
## dmat4 mul ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 )

Matrix multiplication.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## vec2 mul ( vec2 & ret , const dmat4 & m , const vec2 & v )

Matrix by vector multiplication.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec2 mul ( vec2 & ret , const vec2 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec3 mul ( vec3 & ret , const dmat4 & m , const vec3 & v )

Matrix by vector multiplication.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec3 mul ( vec3 & ret , const vec3 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec4 mul ( vec4 & ret , const dmat4 & m , const vec4 & v )

Matrix by vector multiplication.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec4 mul ( vec4 & ret , const vec4 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec2 mul ( vec2 & ret , const dmat4 & m , const dvec2 & v )

Matrix by vector multiplication.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec2 mul ( vec2 & ret , const dvec2 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec3 mul ( vec3 & ret , const dmat4 & m , const dvec3 & v )

Matrix by vector multiplication.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec3 mul ( vec3 & ret , const dvec3 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec4 mul ( vec4 & ret , const dmat4 & m , const dvec4 & v )

Matrix by vector multiplication.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec4 mul ( vec4 & ret , const dvec4 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec2 mul ( dvec2 & ret , const dmat4 & m , const dvec2 & v )

Matrix by vector multiplication.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec2 mul ( dvec2 & ret , const dvec2 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec3 mul ( dvec3 & ret , const dmat4 & m , const dvec3 & v )

Matrix by vector multiplication.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec3 mul ( dvec3 & ret , const dvec3 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec4 mul ( dvec4 & ret , const dmat4 & m , const dvec4 & v )

Matrix by vector multiplication.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec4 mul ( dvec4 & ret , const dvec4 & v , const dmat4 & m )

Vector by matrix multiplication.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec2 mul3 ( vec2 & ret , const dmat4 & m , const vec2 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec2 mul3 ( vec2 & ret , const vec2 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec3 mul3 ( vec3 & ret , const dmat4 & m , const vec3 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec3 mul3 ( vec3 & ret , const vec3 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec4 mul3 ( vec4 & ret , const dmat4 & m , const vec4 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec4 mul3 ( vec4 & ret , const vec4 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec2 mul3 ( vec2 & ret , const dmat4 & m , const dvec2 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec2 mul3 ( vec2 & ret , const dvec2 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec3 mul3 ( vec3 & ret , const dmat4 & m , const dvec3 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec3 mul3 ( vec3 & ret , const dvec3 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## vec4 mul3 ( vec4 & ret , const dmat4 & m , const dvec4 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## vec4 mul3 ( vec4 & ret , const dvec4 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec2 mul3 ( dvec2 & ret , const dmat4 & m , const dvec2 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec2 mul3 ( dvec2 & ret , const dvec2 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec3 mul3 ( dvec3 & ret , const dmat4 & m , const dvec3 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec3 mul3 ( dvec3 & ret , const dvec3 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dvec4 mul3 ( dvec4 & ret , const dmat4 & m , const dvec4 & v )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting vector.
## dvec4 mul3 ( dvec4 & ret , const dvec4 & v , const dmat4 & m )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - The vector to store the result.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

The resulting vector.
## dmat4 mul3 ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 mul4 ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 )

Returns the result of multiplication of the specified arguments.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 mult ( dmat4 & ret , const dmat4 & m , const dvec3 & v )

Returns the matrix with the translation (the last column) multiplied by the specified vector.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

The resulting matrix.
## dmat4 add ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 )

Performs addition with the specified arguments.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 sub ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 )

Subtracts each element in the second argument from its corresponding element in the first argument.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
