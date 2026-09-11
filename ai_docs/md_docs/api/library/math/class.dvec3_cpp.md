# Unigine::Math::dvec3 Struct (CPP)

**Header:** #include <UnigineMathLibDVec3.h>


This class represents a vector of 3 double components.

> **Warning:** Do not use the fourth component in the structure (*align*) as it may be implicitly changed by the structure�s operations.


## dvec3 Struct

### Members

---

## dvec3 ( const hvec3& v )

Constructor. Initializes the vector using a given [hvec3](../../../api/library/math/class.hvec3_cpp.md) source vector.
### Arguments

- *const hvec3&* **v** - Source vector.

## dvec3 ( )

Default constructor. Produces a zero vector.
## dvec3 ( const dvec3& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const dvec3&* **v** - Source vector.

## dvec3 ( const dvec2& v , double z )

Constructor. Initializes the vector using given two-component [dvec2](../../../api/library/math/class.vec2_cpp.md) source vector and a scalar.
### Arguments

- *const dvec2&* **v** - Two-component source vector.
- *double* **z** - Z component of the vector.

## dvec3 ( double x , double y , double z )

Constructor. Initializes the vector using given double values.
### Arguments

- *double* **x** - X component of the vector.
- *double* **y** - Y component of the vector.
- *double* **z** - Z component of the vector.

## explicit dvec3 ( double v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *double* **v** - Scalar value.

## explicit dvec3 ( const dvec2& v )

Constructor. Initializes the vector using a given two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector: x=v.x, y=v.y, z=0.0f.
### Arguments

- *const dvec2&* **v** - Two-component source vector.

## explicit dvec3 ( const dvec4& v )

Constructor. Initializes the vector using a given four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector: x=v.x, y=v.y, z=v.z.
### Arguments

- *const dvec4&* **v** - Four-component source vector.

## explicit dvec3 ( const vec3& v )

Constructor. Initializes the vector using a given [vec3](../../../api/library/math/class.ivec3_cpp.md) source vector.
### Arguments

- *const vec3&* **v** - Source vector.

## explicit dvec3 ( const ivec3& v )

Constructor. Initializes the vector using a given [ivec3](../../../api/library/math/class.ivec3_cpp.md) source vector.
### Arguments

- *const ivec3&* **v** - Source vector.

## explicit dvec3 ( const double* v )

Constructor. Initializes the vector using a given pointer to the array of double elements: x=v[0], y=v[1], z=v[2].
### Arguments

- *const double** **v** - Pointer to the array of double elements.

## dvec3 ( const __m128d& v0 , const __m128d& v1 )

Constructor. Initializes the vector using two [__m128d](https://docs.microsoft.com/en-us/cpp/cpp/m128d?view=msvc-160) (4 floats) variables.

> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.

### Arguments

- *const __m128d&* **v0** - X and Y components of the vector in __m128d format.
- *const __m128d&* **v1** - Z component of the vector in __m128d format (along with alignment).

## explicit dvec3 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *float* **v** - Scalar value.

## dvec3 ( double x , double y , double z , ConstexprTag )

Constructor. Initializes the vector using given *constant* double values.
### Arguments

- *double* **x** - X component of the vector.
- *double* **y** - Y component of the vector.
- *double* **z** - Z component of the vector.
- *ConstexprTag*  - Auxiliary tag.

## dvec3 ( double v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v, z=v.
### Arguments

- *double* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## dvec3 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( double x_ , double y_ , double z_ )

Sets the vector by components.
### Arguments

- *double* **x_** - X component of the vector.
- *double* **y_** - Y component of the vector.
- *double* **z_** - Z component of the vector.

## void set ( const double* val )

Sets the vector using the array of double elements: x=val[0], y=val[1], z=val[2].
### Arguments

- *const double** **val** - Pointer to the array of double elements.

## void set ( const dvec2& val , double z_ )

Sets the vector using a two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector and a scalar.
### Arguments

- *const dvec2&* **val** - Two-component source vector.
- *double* **z_** - Scalar.

## void set ( const dvec3& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const dvec3&* **val** - Source vector.

## void set ( double val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val.
### Arguments

- *double* **val** - Scalar.

## void get ( double* val ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z.
### Arguments

- *double** **val** - Pointer to the array of float elements.

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
## dvec3 & normalize ( )

Returns normalized vector.
### Return value

Normalized vector.
## dvec3 & normalizeValid ( )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## const double * operator const double * ( ) const

Performs type conversion to const double *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## double * operator double * ( )

Performs type conversion to double *.
## void * operator void * ( )

Performs type conversion to void *.
## dvec3 & operator*= ( double v )

Performs scalar multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
## dvec3 & operator*= ( const dvec3& v )

Performs vector multiplication.
### Arguments

- *const dvec3&* **v** - Vector.

### Return value

Resulting vector.
## dvec3 & operator+= ( const dvec3& v )

Performs vector addition.
### Arguments

- *const dvec3&* **v** - Vector.

### Return value

Resulting vector.
## dvec3 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## dvec3 & operator-= ( const dvec3& v )

Performs vector subtraction.
### Arguments

- *const dvec3&* **v** - Vector.

### Return value

Resulting vector.
## dvec3 & operator-= ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## dvec3 & operator/= ( const dvec3& v )

Performs componentwise division of vectors.
### Arguments

- *const dvec3&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
dvec3 a, b;
a = dvec3(6.0, 10.0, 12.0);
b = dvec3(2.0, 5.0, 6.0);
a /= b;
/*
Initial values of vectors a and b:
	a (6.0, 10.0, 12.0)
	b (2.0, 5.0, 6.0)

	a /= b;
Vector a after operation:
	a (3.0, 2.0, 2.0)
*/

```


## dvec3 & operator/= ( double v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
dvec3 a = dvec3(6.0, 10.0, 12.0);
a /= 2.0;
/*
Initial value of vector a:
	a (6.0, 10.0, 12.0)

	a /= 2.0;
Vector a after operation:
	a (3.0, 5.0, 6.0)
*/

```


## dvec3 & operator= ( const dvec3& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const dvec3&* **v** - Source vector.

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

- *double* **v** - Vector multiplier.

## void mul ( const dvec3& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const dvec3&* **v** - Vector multiplier.

## void div ( double v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *double* **v** - A *double* divisor value.

## void div ( const dvec3& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const dvec3&* **v** - A *dvec3* divisor value.

## void add ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## void add ( const dvec3& v )

Performs addition of the specified value.
### Arguments

- *const dvec3&* **v** - Value.

## dvec3 & operator+= ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## void sub ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## void sub ( const dvec3& v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *const dvec3&* **v** - Value.

## double sum ( ) const

Returns the sum of vector components.
## double iLength ( ) const

Returns the inverted length of the vector.
### Return value

Inverted length.
## double maxXY ( ) const

Returns the maximum of X and Y components.
## double max ( ) const

Returns the maximum of X, Y, and Z components.
## double minXY ( )

Returns the minimum of X and Y components.
## double min ( )

Returns the minimum of X, Y, and Z components.
## dvec3 sign ( ) const

Returns the sign of all components as a dvec3 vector. If the sign of the component is more or equals **0**, then the corresponding component of the result vector is **1.0**; otherwise **-1.0**.
### Return value

Result vector.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
