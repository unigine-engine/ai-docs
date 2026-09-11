# Unigine::Math::dvec2 Struct (CPP)

**Header:** #include <UnigineMathLibDVec2.h>


This class represents a vector of 2 double components.


## dvec2 Struct

### Members

---

## dvec2 ( const __m128d& v )


Constructor. Initializes the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128d&* **v** - 128-bit variable.

## dvec2 ( const hvec2& v )

Constructor. Initializes the vector using a given [hvec2](../../../api/library/math/class.hvec2_cpp.md) source vector.
### Arguments

- *const hvec2&* **v** - Source vector.

## dvec2 ( )

Default constructor. Produces a zero vector.
## dvec2 ( const dvec2& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const dvec2&* **v** - Source vector.

## dvec2 ( double x , double y )

Constructor. Initializes the vector using given double values.
### Arguments

- *double* **x** - X component of the vector.
- *double* **y** - Y component of the vector.

### Examples


```cpp
dvec2(2.0, 3.0);
/*
Creates a vector (2.0, 3.0)
*/

```


## explicit dvec2 ( double v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v.
### Arguments

- *double* **v** - Scalar value.

### Examples


```cpp
dvec2(1.0);
/*
Creates a vector (1.0, 1.0)
*/

```


## explicit dvec2 ( const dvec3& v )

Constructor. Initializes the vector using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector: x=v.x, y=v.y.
### Arguments

- *const dvec3&* **v** - Three-component source vector.

## explicit dvec2 ( const dvec4& v )

Constructor. Initializes the vector using a given four-component [vec4](../../../api/library/math/class.vec4_cpp.md) source vector: x=v.x, y=v.y.
### Arguments

- *const dvec4&* **v** - Four-component source vector.

## explicit dvec2 ( const vec2& v )

Constructor. Initializes the vector using a given [vec2](../../../api/library/math/class.vec2_cpp.md) source vector.
### Arguments

- *const vec2&* **v** - Source vector.

## explicit dvec2 ( const ivec2& v )

Constructor. Initializes the vector using a given [ivec2](../../../api/library/math/class.ivec2_cpp.md) source vector.
### Arguments

- *const ivec2&* **v** - Source vector.

## explicit dvec2 ( const double* v )

Constructor. Initializes the vector using a given pointer to the array of double elements: x=v[0], y=v[1].
### Arguments

- *const double** **v** - Pointer to the array of double elements.

## dvec2 ( double x , double y , ConstexprTag )

Constructor. Initializes the vector using a given double elements.
### Arguments

- *double* **x** - Source element.
- *double* **y** - Source element.
- *ConstexprTag*  - Auxiliary tag.

## dvec2 ( double v , ConstexprTag )

Constructor. Initializes both vector components using a given double element.
### Arguments

- *double* **v** - Source element.
- *ConstexprTag*  - Auxiliary tag.

## dvec2 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( double x_ , double y_ )

Sets the vector by components.
### Arguments

- *double* **x_** - X component of the vector.
- *double* **y_** - Y component of the vector.

## void set ( const double* val )

Sets the vector using the array of double elements: x=val[0], y=val[1].
### Arguments

- *const double** **val** - Pointer to the array of double elements.

## void set ( double val )

Sets the vector components equal to specified scalar value: x=val, y=val.
### Arguments

- *double* **val** - Scalar value.

## void set ( const dvec2& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const dvec2&* **val** - Source vector.

## void get ( double* val ) const

Gets the vector: val[0]=x, val[1]=y.
### Arguments

- *double** **val** - Pointer to the array of double elements.

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
## double iLength ( ) const

Returns the inverted length of the vector.
### Return value

Inverted length.
## const double * operator const double * ( ) const

Performs type conversion to const double *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## double * operator double * ( )

Performs type conversion to double *.
## void * operator void * ( )

Performs type conversion to void *.
## dvec2 & operator*= ( double v )

Performs scalar multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
## dvec2 & operator*= ( const dvec2& v )

Performs vector multiplication.
### Arguments

- *const dvec2&* **v** - Vector.

### Return value

Resulting vector.
## dvec2 & operator+= ( const dvec2& v )

Performs vector addition.
### Arguments

- *const dvec2&* **v** - Vector.

### Return value

Resulting vector.
## dvec2 & operator+= ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## dvec2 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## dvec2 & operator-= ( const dvec2& v )

Performs vector subtraction.
### Arguments

- *const dvec2&* **v** - Vector.

### Return value

Resulting vector.
## dvec2 & operator-= ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## dvec2 & operator/= ( double v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *double* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
dvec2 a = dvec2(6.0, 10.0);
a /= 2.0;
/*
Initial value of vector a:
	a (6.0, 10.0)

	a /= 2.0;
Vector a after operation:
	a (3.0, 5.0)
*/

```


## dvec2 & operator/= ( const dvec2& v )

Performs componentwise division of vectors.
### Arguments

- *const dvec2&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
dvec2 a, b;
a = dvec2(6.0, 10.0);
b = dvec2(2.0, 5.0);
a /= b;
/*
Initial values of vectors a and b:
	a (6.0, 10.0)
	b (2.0, 5.0)

	a /= b;
Vector a after operation:
	a (3.0, 2.0)
*/

```


## dvec2 & operator= ( const dvec2& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const dvec2&* **v** - Source vector.

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

## void mul ( const dvec2& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const dvec2&* **v** - Vector multiplier.

## void div ( double v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *double* **v** - A *double* divisor value.

## void div ( const dvec2& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const dvec2&* **v** - A *dvec2* divisor value.

## void sub ( double v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *double* **v** - Value.

## void sub ( const dvec2& v )

Subtracts each element of the specified value from the corresponding vector's element.
### Arguments

- *const dvec2&* **v** - Value.

## double sum ( ) const

Returns the sum of vector components.
## void add ( double v )

Performs addition of the specified value.
### Arguments

- *double* **v** - Value.

## void add ( const dvec2& v )

Performs addition of the specified value.
### Arguments

- *const dvec2&* **v** - Value.

## double max ( ) const

Returns the maximum value among all components.
### Return value

Maximum value.
## double min ( ) const

Returns the minimum value among all components.
### Return value

Minimum value.
## dvec2 frac ( ) const

Returns a vector containing fractional parts of the corresponding vector components.
### Return value

Fractional parts of the corresponding vector components.
## ivec2 floor ( ) const

Returns a vector containing the largest integral values each being less than or equal to the corresponding vector component.
### Return value

Vector containing the largest integral values.
## ivec2 ceil ( ) const

Returns a vector containing the smallest integral values each being greater than or equal to the corresponding vector component.
### Return value

Vector containing the smallest integral values.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
