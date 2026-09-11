# Unigine::Math::dvec4 Struct (CPP)

**Header:** #include <UnigineMathLibDVec4.h>


This class represents a vector of 4 double components.


## dvec4 Struct

### Members

---

## dvec4 ( const hvec4& v )

Constructor. Initializes the vector using a given [hvec4](../../../api/library/math/class.hvec4_cpp.md) source vector.
### Arguments

- *const hvec4&* **v** - Source vector.

## dvec4 ( )

Default constructor. Produces a zero vector.
## dvec4 ( const dvec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## dvec4 ( const dvec2& v , double z , double w )

Constructor. Initializes the vector using a given two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector and two scalars.
### Arguments

- *const dvec2&* **v** - Two-component source vector.
- *double* **z** - Z component of the vector.
- *double* **w** - W component of the vector.

## dvec4 ( const dvec3& v , double w )

Constructor. Initializes the vector using a given three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector and a scalar.
### Arguments

- *const dvec3&* **v** - Three-component source vector.
- *double* **w** - W component of the vector.

## dvec4 ( double x , double y , double z , double w )

Constructor. Initializes the vector using given double values.
### Arguments

- *double* **x** - X component of the vector.
- *double* **y** - Y component of the vector.
- *double* **z** - Z component of the vector.
- *double* **w** - W component of the vector.

### Examples


```cpp
dvec4(1.0, 2.0, 3.0, 4.5);
/*
Creates a vector (1.0, 2.0, 3.0, 4.5)
*/

```


## explicit dvec4 ( double v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *double* **v** - Scalar value.

## explicit dvec4 ( const dvec2& v )

Constructor. Initializes the vector using a given two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector: x=v.x, y=v.y, z=0.0f, w=1.0f.
### Arguments

- *const dvec2&* **v** - Two-component source vector.

## explicit dvec4 ( const dvec3& v )

Constructor. Initializes the vector using a given three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector: x=v.x, y=v.y, z=v.z, w=1.0f.
### Arguments

- *const dvec3&* **v** - Three-component source vector.

## explicit dvec4 ( const vec4& v )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## explicit dvec4 ( const ivec4& v )

Constructor. Initializes the vector using a given [ivec4](../../../api/library/math/class.ivec4_cpp.md) source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## explicit dvec4 ( const bvec4& v )

Constructor. Initializes the vector using a given [bvec4](../../../api/library/math/class.bvec4_cpp.md) source vector.
### Arguments

- *const bvec4&* **v** - Source vector.

## explicit dvec4 ( const svec4& v )

Constructor. Initializes the vector using a given [svec4](../../../api/library/math/class.svec4_cpp.md) source vector.
### Arguments

- *const svec4&* **v** - Source vector.

## explicit dvec4 ( const double* v )

Constructor. Initializes the vector using a given pointer to the array of double elements: x=v[0], y=v[1], z=v[2], w=v[3].
### Arguments

- *const double** **v** - Pointer to the array of double elements.

## dvec4 ( const __m128d& v0 , const __m128d& v1 )

Constructor. Initializes the vector using two [__m128d](https://docs.microsoft.com/en-us/cpp/cpp/m128d?view=msvc-160) variables.

> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.

### Arguments

- *const __m128d&* **v0** - X and Y components of the vector in __m128d format.
- *const __m128d&* **v1** - Z and W components of the vector in __m128d format.

## dvec4 ( const dvec2& v0 , const dvec2& v1 )

Constructor. Initializes the vector using two [dvec2](../../../api/library/math/class.dvec2_cpp.md) vectors.
### Arguments

- *const dvec2&* **v0** - Two-component source vector for X and Y components.
- *const dvec2&* **v1** - Two-component source vector for Z and W components.

## dvec4 ( double x , double y , double z , double w , ConstexprTag )

Constructor. Initializes the vector using given *constant* double values.
### Arguments

- *double* **x** - X component of the vector.
- *double* **y** - Y component of the vector.
- *double* **z** - Z component of the vector.
- *double* **w** - W component of the vector.
- *ConstexprTag*  - Auxiliary tag.

## dvec4 ( double v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *double* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## dvec4 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( double x_ , double y_ , double z_ , double w_ )

Sets the vector by components.
### Arguments

- *double* **x_** - X component of the vector.
- *double* **y_** - Y component of the vector.
- *double* **z_** - Z component of the vector.
- *double* **w_** - W component of the vector.

## void set ( const double* v )

Sets the vector using the array of double elements: x=val[0], y=val[1], z=val[2], w=val[3].
### Arguments

- *const double** **v** - Pointer to the array of double elements.

## void set ( const dvec4& v )

Sets the vector equal to the specified source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## void set ( const dvec3& v , double w_ )

Sets the vector using a three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector and a scalar.
### Arguments

- *const dvec3&* **v** - Three-component source vector.
- *double* **w_** - W component of the vector.

## void set ( double v )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *double* **v** - Scalar value.

## void set ( const dvec2& v , double z_ , double w_ )

Sets the vector using a two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector and two scalars.
### Arguments

- *const dvec2&* **v** - Two-component source vector.
- *double* **z_** - Z component of the vector.
- *double* **w_** - W component of the vector.

## void get ( double* v ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z, val[3]=w.
### Arguments

- *double** **v** - Pointer to the array of double elements.

## double * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const double * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## double length ( ) const

Returns the length of the vector.
### Return value

Vector length.
## double length2 ( ) const

Returns the squared length of the vector.
### Return value

Squared length of the vector.
## dvec4 & normalize ( )

Returns normalized vector.
### Return value

Normalized vector.
## dvec4 & normalizeValid ( )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## dvec4 & normalize3 ( )

Returns the vector with normalized XYZ components.
### Return value

Vector with normalized XYZ components.
## dvec4 & normalizeValid3 ( )

Returns the vector with normalized XYZ components. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Vector with normalized XYZ components.
## const double * operator const double * ( ) const

Performs type conversion to const double *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## double * operator double * ( )

Performs type conversion to double *.
## void * operator void * ( )

Performs type conversion to void *.
## dvec4 & operator*= ( double v )

Performs scalar multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
## dvec4 & operator*= ( const dvec4& v )

Performs vector multiplication.
### Arguments

- *const dvec4&* **v** - Vector.

### Return value

Resulting vector.
## dvec4 & operator+= ( const dvec4& v )

Performs vector addition.
### Arguments

- *const dvec4&* **v** - Vector.

### Return value

Resulting vector.
## dvec4 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## dvec4 & operator-= ( const dvec4& v )

Performs vector subtraction.
### Arguments

- *const dvec4&* **v** - Vector.

### Return value

Resulting vector.
## dvec4 & operator/= ( const dvec4& v )

Performs componentwise division of vectors.
### Arguments

- *const dvec4&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
dvec4 a, b;
a = dvec4(6.0, 10.0, 12.0, 25.0);
b = dvec4(2.0, 5.0, 6.0, 5.0);
a /= b;
/*
Initial values of vectors a and b:
	a (6.0, 10.0, 12.0, 25.0)
	b (2.0, 5.0, 6.0, 5.0)

	a /= b;
Vector a after operation:
	a (3.0, 2.0, 2.0, 5.0)
*/

```


## dvec4 & operator/= ( double v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
dvec4 a = dvec4(6.0, 10.0, 12.0, 25.0);
a /= 2.0;
/*
Initial value of vector a:
	a (6.0, 10.0, 12.0, 25.0)

	a /= 2.0;
Vector a after operation:
	a (3.0, 5.0, 6.0, 12.5)
*/

```


## dvec4 & operator= ( const dvec4& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

### Return value

Result.
## double & operator[] ( int i )

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## double operator[] ( int i ) const

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
## void mul ( double v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *double* **v** - A *double* multiplier.

## void mul ( const dvec4& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const dvec4&* **v** - Vector multiplier.

## void mul3 ( double v )

Multiplies the X, Y, and Z components of the vector by the value of the specified argument.
### Arguments

- *double* **v** - A *double* multiplier.

## void div ( double v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *double* **v** - A *double* divisor value.

## void div ( const dvec4& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const dvec4&* **v** - A *dvec4* divisor value.

## double sum ( ) const

Returns the sum of vector components.
## void add ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## void add ( const dvec4& v )

Performs addition of the specified value.
### Arguments

- *const dvec4&* **v** - Value.

## dvec4 & operator+= ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## void sub ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## void sub ( const dvec4& v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *const dvec4&* **v** - Value.

## dvec4 & operator-= ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## double iLength ( ) const

Returns the inverted length of the vector.
## double maxXY ( ) const

Returns the maximum of X and Y components.
## double maxXYZ ( ) const

Returns the maximum of X, Y, and Z components.
## double max ( ) const

Returns the maximum of X, Y, Z, and W components.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
