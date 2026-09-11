# Unigine::Math::ivec3 Struct (CPP)

**Header:** #include <UnigineMathLibIVec3.h>


This class represents a vector of 3 integer components.

> **Warning:** Do not use the fourth component in the structure (*align*) as it may be implicitly changed by the structure�s operations.


## ivec3 Struct

### Members

---

## ivec3 ( const __m128i& v )


Constructor. Initializes the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128i&* **v** - 128-bit variable

## ivec3 ( )

Default constructor. Produces a zero vector.
## ivec3 ( const ivec3& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const ivec3&* **v** - Source vector.

## ivec3 ( int x , int y , int z )

Constructor. Initializes the vector using given integer values.
### Arguments

- *int* **x** - X component of the vector.
- *int* **y** - Y component of the vector.
- *int* **z** - Z component of the vector.

### Examples


```cpp
ivec2(2, 3, 4);
/*
Creates a vector (2, 3, 4)
*/

```


## explicit ivec3 ( int v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *int* **v** - Scalar value.

## explicit ivec3 ( const vec3& v )

Constructor. Initializes the vector using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.
### Arguments

- *const vec3&* **v** - Source vector.

## explicit ivec3 ( const dvec3& v )

Constructor. Initializes the vector using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.
### Arguments

- *const dvec3&* **v** - Source vector.

## explicit ivec3 ( const int* v )

Constructor. Initializes the vector using a given pointer to the array of integer elements: x=v[0], y=v[1], z=v[2].
### Arguments

- *const int** **v** - Pointer to the array of integer elements.

## ivec3 ( const ivec4& v )

Constructor. Initializes the vector using a given [ivec4](../../../api/library/math/class.ivec4_cpp.md) source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## ivec3 ( const ivec2& xy , int z )

### Arguments

- *const ivec2&* **xy**
- *int* **z**

## ivec3 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( int x_ , int y_ , int z_ )

Sets the vector by components.
### Arguments

- *int* **x_** - X component of the vector.
- *int* **y_** - Y component of the vector.
- *int* **z_** - Z component of the vector.

## void set ( const int* val )

Sets the vector using the array of integer elements: x=val[0], y=val[1], z=val[2].
### Arguments

- *const int** **val** - Pointer to the array of integer elements.

## void set ( const ivec3& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const ivec3&* **val** - Source vector.

## void set ( int val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val.
### Arguments

- *int* **val** - Scalar.

## int * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const int * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## void get ( int* val ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z.
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
## ivec3 & operator*= ( int v )

Performs scalar multiplication.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
## ivec3 & operator*= ( const ivec3& v )

Performs vector multiplication.
### Arguments

- *const ivec3&* **v** - Vector.

### Return value

Resulting vector.
## ivec3 & operator+= ( const ivec3& v )

Performs vector addition.
### Arguments

- *const ivec3&* **v** - Vector.

### Return value

Resulting vector.
## ivec3 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## ivec3 & operator-= ( const ivec3& v )

Performs vector subtraction.
### Arguments

- *const ivec3&* **v** - Vector.

### Return value

Resulting vector.
## ivec3 & operator/= ( int v )

Performs componentwise integer division of the vector by the scalar.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
ivec3 a = ivec3(6, 10, 11);
a /= 2;
/*
Initial value of vector a:
	a (6, 10, 11)

	a /= 2;
Vector a after operation:
	a (3, 5, 5)
*/

```


## ivec3 & operator/= ( const ivec3& v )

Performs componentwise integer division of vectors.
### Arguments

- *const ivec3&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
ivec3 a, b;
a = ivec3(6, 10, 12);
b = ivec3(2, 6, 5);
a /= b;
/*
Initial values of vectors a and b:
	a (6, 10, 12)
	b (2, 6, 5)

	a /= b;
Vector a after operation:
	a (3, 1, 2)

```


## ivec3 & operator<<= ( int v )

Performs componentwise left bit shift.
### Arguments

- *int* **v** - Shift amount.

### Return value

Resulting vector.
## ivec3 & operator= ( const ivec3& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const ivec3&* **v** - Source vector.

### Return value

Result.
## ivec3 & operator= ( const __m128i& val )


Sets the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128i&* **val** - 128-bit variable.

### Return value

Vector.
## ivec3 & operator>>= ( int v )

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
## int mul ( ) const

Multiplies the vector by the value of the specified argument.
### Return value

Vector multiplier.
## void mul ( int v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *int* **v** - An *int* multiplier.

## void mul ( const ivec3& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const ivec3&* **v** - Vector multiplier.

## void div ( int v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *int* **v** - An *int* divisor value.

## void div ( const ivec3& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const ivec3&* **v** - A *ivec3* divisor value.

## void sub ( int v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *int* **v** - Value.

## void sub ( const ivec3& v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *const ivec3&* **v** - Value.

## ivec3 & operator-= ( int v )

Performs vector subtraction.
### Arguments

- *int* **v** - Value.

## int sum ( ) const

Returns the sum of vector components.
## void add ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void add ( const ivec3& v )

Performs addition of the specified value.
### Arguments

- *const ivec3&* **v** - Value.

## ivec3 & operator+= ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( int v )

Bitwise left shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( const ivec3& v )

Bitwise left shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec3&* **v** - Value.

## ivec3 & operator<<= ( const ivec3& v )

Bitwise left shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec3&* **v** - Value.

### Return value

This vector.
## ivec3 & operator<<= ( int v )

Bitwise left shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

### Return value

This vector.
## void shiftRight ( int v )

Bitwise right shift by a specific value. All components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftRight ( const ivec3& v )

Bitwise right shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec3&* **v** - Value.

## ivec3 & operator>>= ( const ivec3& v )

Bitwise right shift by a specific value. All components are shifted by the value's corresponding component.
### Arguments

- *const ivec3&* **v** - Value.

### Return value

This vector.
## ivec3 & operator>>= ( int v )

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
