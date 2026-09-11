# Unigine::Math::ivec4 Struct (CPP)

**Header:** #include <UnigineMathLibIVec4.h>


This class represents a vector of 4 integer components.


## ivec4 Struct

### Members

---

## ivec4 ( const __m128i& v )

Constructor. Initializes the vector using a [__m128i](https://docs.microsoft.com/en-us/cpp/cpp/m128i?view=msvc-160) variable.

> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.

### Arguments

- *const __m128i&* **v** - All components of the vector in *__m128d* format

## ivec4 ( )

Default constructor. Produces a zero vector.
## ivec4 ( const ivec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## ivec4 ( int x , int y , int z , int w )

Constructor. Initializes the vector using given integer values.
### Arguments

- *int* **x** - X component of the vector.
- *int* **y** - Y component of the vector.
- *int* **z** - Z component of the vector.
- *int* **w** - W component of the vector.

## explicit ivec4 ( int v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *int* **v** - Scalar value.

## explicit ivec4 ( const vec4& v )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## explicit ivec4 ( const dvec4& v )

Constructor. Initializes the vector using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## explicit ivec4 ( const bvec4& v )

Constructor. Initializes the vector using a given [bvec4](../../../api/library/math/class.bvec4_cpp.md) source vector.
### Arguments

- *const bvec4&* **v** - Source vector.

## explicit ivec4 ( const svec4& v )

Constructor. Initializes the vector using a given [svec4](../../../api/library/math/class.svec4_cpp.md) source vector.
### Arguments

- *const svec4&* **v** - Source vector.

## explicit ivec4 ( const int* v )

Constructor. Initializes the vector using a given pointer to the array of integer elements: x=v[0], y=v[1], z=v[2], w=v[3].
### Arguments

- *const int** **v** - Pointer to the array of integer elements.

## ivec4 ( const ivec3& v )

Constructor. Initializes the vector using a given [ivec3](../../../api/library/math/class.ivec3_cpp.md) source vector.
### Arguments

- *const ivec3&* **v** - Source vector.

## ivec4 ( const ivec2& v0 , const ivec2& v1 )

Constructor. Initializes the vector using given [ivec2](../../../api/library/math/class.ivec2_cpp.md) source vectors.
### Arguments

- *const ivec2&* **v0** - Source vector for X and Y components.
- *const ivec2&* **v1** - Source vector for Z and W components.

## ivec4 ( const ivec2& v , int z , int w )

Constructor. Initializes the vector using a given [ivec2](../../../api/library/math/class.ivec2_cpp.md) source vector and two *int* values for Z and W components.
### Arguments

- *const ivec2&* **v** - Source vector for X and Y components.
- *int* **z** - Z component of the vector.
- *int* **w** - W component of the vector.

## ivec4 ( const ivec3& v , int w )

Constructor. Initializes the vector using a given [ivec3](../../../api/library/math/class.ivec3_cpp.md) source vector and an *int* value for the W component.
### Arguments

- *const ivec3&* **v** - Source vector for X, Y and Z components.
- *int* **w** - W component of the vector.

## ivec4 ( int v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *int* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## ivec4 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( int x_ , int y_ , int z_ , int w_ )

Sets the vector by components.
### Arguments

- *int* **x_** - X component of the vector.
- *int* **y_** - Y component of the vector.
- *int* **z_** - Z component of the vector.
- *int* **w_** - W component of the vector.

## void set ( const int* val )

Sets the vector using the array of integer elements: x=val[0], y=val[1], z=val[2], w=val[3].
### Arguments

- *const int** **val** - Pointer to the array of integer elements.

## void set ( int val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *int* **val** - Scalar value.

## void set ( const ivec4& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const ivec4&* **val** - Source vector.

## int * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const int * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## void get ( int* val ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z, val[3]=w.
### Arguments

- *int** **val** - Pointer to the array of integer elements.

## int length2 ( ) const

Returns the squared length of the vector.
### Return value

Squared length of the vector.
## const int * operator const int * ( ) const

Performs type conversion to const int *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## int * operator int * ( )

Performs type conversion to int *.
## void * operator void * ( )

Performs type conversion to void *.
## ivec4 & operator*= ( int v )

Performs scalar multiplication.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
## ivec4 & operator*= ( const ivec4& v )

Performs vector multiplication.
### Arguments

- *const ivec4&* **v** - Vector.

### Return value

Resulting vector.
## ivec4 & operator+= ( const ivec4& v )

Performs vector addition.
### Arguments

- *const ivec4&* **v** - Vector.

### Return value

Resulting vector.
## ivec4 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## ivec4 & operator-= ( const ivec4& v )

Performs vector subtraction.
### Arguments

- *const ivec4&* **v** - Vector.

### Return value

Resulting vector.
## ivec4 & operator/= ( int v )

Performs componentwise integer division of the vector by the scalar.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
ivec4 a = ivec4(6, 10, 11, 4);
a /= 2;
/*
Initial value of vector a:
	a (6, 10, 11, 4)

	a /= 2;
Vector a after operation:
	a (3, 5, 5, 2)
*/

```


## ivec4 & operator/= ( const ivec4& v )

Performs componentwise integer division of vectors.
### Arguments

- *const ivec4&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
ivec4 a, b;
a = ivec4(6, 10, 12, 3);
b = ivec4(2, 6, 5, 2);
a /= b;
/*
Initial values of vectors a and b:
	a (6, 10, 12, 3)
	b (2, 6, 5, 2)

	a /= b;
Vector a after operation:
	a (3, 1, 2, 1)

```


## ivec4 & operator<<= ( int v )

Performs componentwise left bit shift.
### Arguments

- *int* **v** - Shift amount.

### Return value

Resulting vector.
## ivec4 & operator= ( const __m128i& val )

Performs vector assignment. Destination vector = Source vector.

> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.

### Arguments

- *const __m128i&* **val** - Source vector in the [__m128i](https://docs.microsoft.com/en-us/cpp/cpp/m128i?view=msvc-160) format.

## ivec4 & operator= ( const ivec4& val )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const ivec4&* **val** - Source vector.

### Return value

Result.
## ivec4 & operator>>= ( int v )

Performs componentwise right bit shift.
### Arguments

- *int* **v** - Shift amount.

### Return value

Resulting vector.
## int & operator[] ( int i )

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## int operator[] ( int i ) const

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
## ivec4 & operator= ( int val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *int* **val** - Scalar value.

### Return value

This vector.
## int mul ( ) const

Multiplies the vector by the value of the specified argument.
### Return value

Vector multiplier.
## void mul ( int v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *int* **v** - An *int* multiplier.

## void mul ( const ivec4& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const ivec4&* **v** - Vector multiplier.

## void div ( int v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *int* **v** - An *int* divisor value.

## void div ( const ivec4& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const ivec4&* **v** - A *ivec4* divisor value.

## void sub ( int v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *int* **v** - Value.

## void sub ( const ivec4& v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *const ivec4&* **v** - Value.

## ivec4 & operator-= ( int v )

Performs vector subtraction.
### Arguments

- *int* **v** - Value.

## int sum ( ) const

Returns the sum of vector components.
## void add ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void add ( const ivec4& v )

Performs addition of the specified value.
### Arguments

- *const ivec4&* **v** - Value.

## ivec4 & operator+= ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( int v )

Bitwise left shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( const ivec4& v )

Bitwise left shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec4&* **v** - Value.

## ivec4 & operator<<= ( const ivec4& v )

Bitwise left shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec4&* **v** - Value.

### Return value

This vector.
## ivec4 & operator<<= ( int v )

Bitwise left shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

### Return value

This vector.
## void shiftRight ( int v )

Bitwise right shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftRight ( const ivec4& v )

Bitwise right shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec4&* **v** - Value.

## ivec4 & operator>>= ( const ivec4& v )

Bitwise right shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec4&* **v** - Value.

### Return value

This vector.
## ivec4 & operator>>= ( int v )

Bitwise right shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

### Return value

This vector.
## int max ( ) const

Returns the maximum of all components.
## int min ( ) const

Returns the minimum of all components.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
