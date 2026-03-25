# Unigine::Math::vec2 Struct (CPP)

**Header:** #include <UnigineMathLibVec2.h>


This class represents a vector of 2 float components.


## vec2 Struct

### Members

---

## vec2 ( const hvec2& v )

Constructor. Initializes the vector using a given [hvec2](../../../api/library/math/class.hvec2_cpp.md) source vector.
### Arguments

- *const hvec2&* **v** - Source vector.

## vec2 ( )

Default constructor. Produces a zero vector.
## vec2 ( const vec2& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const vec2&* **v** - Source vector.

## vec2 ( float x , float y )

Constructor. Initializes the vector using given float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.

### Examples


```cpp
vec2(2.0, 3.0);
/*
Creates a vector (2.0, 3.0)
*/

```


## explicit vec2 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v.
### Arguments

- *float* **v** - Scalar value.

### Examples


```cpp
vec2(1.0);
/*
Creates a vector (1.0, 1.0)
*/

```


## explicit vec2 ( const vec3& v )

Constructor. Initializes the vector using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) source vector: x=v.x, y=v.y.
### Arguments

- *const vec3&* **v** - Three-component source vector.

## explicit vec2 ( const vec4& v )

Constructor. Initializes the vector using a given four-component [vec4](../../../api/library/math/class.vec4_cpp.md) source vector: x=v.x, y=v.y.
### Arguments

- *const vec4&* **v** - Four-component source vector.

## explicit vec2 ( const dvec2& v )

Constructor. Initializes the vector using a given [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector.
### Arguments

- *const dvec2&* **v** - Source vector.

## explicit vec2 ( const ivec2& v )

Constructor. Initializes the vector using a given [ivec2](../../../api/library/math/class.ivec2_cpp.md) source vector.
### Arguments

- *const ivec2&* **v** - Source vector.

## explicit vec2 ( const float* v )

Constructor. Initializes the vector using a given pointer to the array of float elements: x=v[0], y=v[1].
### Arguments

- *const float** **v** - Pointer to the array of float elements.

## vec2 ( float x , float y , ConstexprTag )

Constructor. Initializes the vector using given *constant* float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.
- *ConstexprTag*  - Auxiliary tag.

## vec2 ( float v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v.
### Arguments

- *float* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## vec2 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( float x_ , float y_ )

Sets the vector by components.
### Arguments

- *float* **x_** - X component of the vector.
- *float* **y_** - Y component of the vector.

## void set ( const float* val )

Sets the vector using the array of float elements: x=val[0], y=val[1].
### Arguments

- *const float** **val** - Pointer to the array of float elements.

## void set ( const vec2& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const vec2&* **val** - Source vector.

## void set ( float val )

Sets the vector components equal to specified scalar value: x=val, y=val.
### Arguments

- *float* **val** - Scalar value.

## void get ( float* val ) const

Gets the vector: val[0]=x, val[1]=y.
### Arguments

- *float** **val** - Pointer to the array of float elements.

## float * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const float * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## float length ( ) const

Returns the length of the vector.
### Return value

Vector length.
## float length2 ( ) const

Returns the squared length of the vector.
### Return value

Squared length of the vector.
## float max ( ) const

Compares the vector components and returns the greater one.
### Return value

The greater out of the two vector components.
## vec2 & normalize ( )

Returns normalized vector.
### Return value

Normalized vector.
## vec2 & normalizeValid ( )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## vec2 & normalizeFast ( )

Returns normalized vector, calculated using the fast inverse square root algorithm.
### Return value

Normalized vector.
## vec2 & normalizeValidFast ( )

Returns normalized vector, calculated using the fast inverse square root algorithm. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## const float * operator const float * ( ) const

Performs type conversion to const float *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## float * operator float * ( )

Performs type conversion to float *.
## void * operator void * ( )

Performs type conversion to void *.
## vec2 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
## vec2 & operator*= ( const vec2& v )

Performs vector multiplication.
### Arguments

- *const vec2&* **v** - Vector.

### Return value

Resulting vector.
## vec2 & operator+= ( const vec2& v )

Performs vector addition.
### Arguments

- *const vec2&* **v** - Vector.

### Return value

Resulting vector.
## vec2 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## vec2 & operator-= ( const vec2& v )

Performs vector subtraction.
### Arguments

- *const vec2&* **v** - Vector.

### Return value

Resulting vector.
## vec2 & operator/= ( const vec2& v )

Performs componentwise division of vectors.
### Arguments

- *const vec2&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
vec2 a, b;
a = vec2(6.0, 10.0);
b = vec2(2.0, 5.0);
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


## vec2 & operator/= ( float v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
vec2 a = vec2(6.0, 10.0);
a /= 2.0;
/*
Initial value of vector a:
	a (6.0, 10.0)

	a /= 2.0;
Vector a after operation:
	a (3.0, 5.0)
*/

```


## vec2 & operator= ( const vec2& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const vec2&* **v** - Source vector.

### Return value

Result.
## float & operator[] ( int i )

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## float operator[] ( int i ) const

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
## void mul ( float v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *float* **v** - A *float* multiplier.

## void mul ( const vec2& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const vec2&* **v** - Vector multiplier.

## void div ( float v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - A *float* divisor value.

## void div ( const vec2& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const vec2&* **v** - A *vec2* divisor value.

## vec2 & operator/= ( float v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## vec2 & operator/= ( const ivec2& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const ivec2&* **v** - Value.

### Return value

This vector.
## void sub ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

## void sub ( const vec2& v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *const vec2&* **v** - Value.

## vec2 & operator-= ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## float sum ( ) const

Returns the sum of vector components.
## void add ( float v )

Performs addition of the specified argument.
### Arguments

- *float* **v** - Value.

## void add ( const vec2& v )

Performs addition of the specified argument.
### Arguments

- *const vec2&* **v** - Value.

## vec2 & operator+= ( float v )

Performs addition of the specified value.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## float iLength ( ) const

Returns the inverted length of the vector.
## float iLengthFast ( ) const

Returns the inverted length of the vector (fast version).
## vec2 frac ( ) const

Returns a vector containing fractional parts of the corresponding vector components.
## float min ( ) const

Returns the minimum value among all components.
## ivec2 floor ( ) const

Returns a vector containing the largest integral values each being less than or equal to the corresponding vector component.
## ivec2 ceil ( ) const

Returns a vector containing the smallest integral values each being greater than or equal to the corresponding vector component.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
