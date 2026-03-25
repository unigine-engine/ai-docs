# Unigine::Math::ivec2 Struct (CPP)

**Header:** #include <UnigineMathLibIVec2.h>


This class represents a vector of 2 integer components.


## ivec2 Struct

### Members

---

## ivec2 ( )

Default constructor. Produces a zero vector.
## ivec2 ( const ivec2& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const ivec2&* **v** - Source vector.

## ivec2 ( int x , int y )

Constructor. Initializes the vector using given integer values.
### Arguments

- *int* **x** - X component of the vector.
- *int* **y** - Y component of the vector.

### Examples


```cpp
ivec2(2, 3);
/*
Creates a vector (2, 3)
*/

```


## explicit ivec2 ( int v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v.
### Arguments

- *int* **v** - Scalar value.

### Examples


```cpp
ivec2(1);
/*
Creates a vector (1, 1)
*/

```


## explicit ivec2 ( const vec2& v )

Constructor. Initializes the vector using a given [vec2](../../../api/library/math/class.vec2_cpp.md) source vector.
### Arguments

- *const vec2&* **v** - Source vector.

## explicit ivec2 ( const dvec2& v )

Constructor. Initializes the vector using a given [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vector.
### Arguments

- *const dvec2&* **v** - Source vector.

## explicit ivec2 ( const int* v )

Constructor. Initializes the vector using a given pointer to the array of integer elements: x=v[0], y=v[1].
### Arguments

- *const int** **v** - Pointer to the array of integer elements.

## ivec2 ( int v , ConstexprTag )

### Arguments

- *int* **v**
- *ConstexprTag*

## ivec2 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( int x_ , int y_ )

Sets the vector by components.
### Arguments

- *int* **x_** - X component of the vector.
- *int* **y_** - Y component of the vector.

## void set ( const int* val )

Sets the vector using the array of integer elements: x=val[0], y=val[1].
### Arguments

- *const int** **val** - Pointer to the array of integer elements.

## void set ( const ivec2& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const ivec2&* **val** - Source vector.

## void set ( int val )

Sets the vector components equal to specified scalar value: x=val, y=val.
### Arguments

- *int* **val** - Scalar value.

## int * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const int * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## void get ( int* val ) const

Gets the vector: val[0]=x, val[1]=y.
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
## ivec2 & operator*= ( int v )

Performs scalar multiplication.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
## ivec2 & operator*= ( const ivec2& v )

Performs vector multiplication.
### Arguments

- *const ivec2&* **v** - Vector.

### Return value

Resulting vector.
## ivec2 & operator+= ( const ivec2& v )

Performs vector addition.
### Arguments

- *const ivec2&* **v** - Vector.

### Return value

Resulting vector.
## ivec2 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## ivec2 & operator-= ( const ivec2& v )

Performs vector subtraction.
### Arguments

- *const ivec2&* **v** - Vector.

### Return value

Resulting vector.
## ivec2 & operator/= ( int v )

Performs componentwise integer division of the vector by the scalar.
### Arguments

- *int* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
ivec2 a = ivec2(6, 10);
a /= 2;
/*
Initial value of vector a:
	a (6, 10)

	a /= 2;
Vector a after operation:
	a (3, 5)
*/

```


## ivec2 & operator/= ( const ivec2& v )

Performs componentwise integer division of vectors.
### Arguments

- *const ivec2&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
ivec2 a, b;
a = ivec2(6, 10);
b = ivec2(2, 6);
a /= b;
/*
Initial values of vectors a and b:
	a (6, 10)
	b (2, 6)

	a /= b;
Vector a after operation:
	a (3, 1)

```


## ivec2 & operator<<= ( int v )

Performs componentwise left bit shift.
### Arguments

- *int* **v** - Shift amount.

### Return value

Resulting vector.
## ivec2 & operator= ( const ivec2& val )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const ivec2&* **val** - Source vector.

### Return value

Result.
## ivec2 & operator>>= ( int v )

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

## void mul ( const ivec2& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const ivec2&* **v** - Vector multiplier.

## void div ( int v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *int* **v** - An *int* divisor value.

## void div ( const ivec2& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const ivec2&* **v** - A *ivec2* divisor value.

## void sub ( int v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *int* **v** - Value.

## void sub ( const ivec2& v )

Subtracts each element of the specified argument from the corresponding element.
### Arguments

- *const ivec2&* **v** - Value.

## ivec2 & operator-= ( int v )

Performs vector subtraction.
### Arguments

- *int* **v** - Value.

## int sum ( ) const

Returns the sum of vector components.
## void add ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void add ( const ivec2& v )

Performs addition of the specified value.
### Arguments

- *const ivec2&* **v** - Value.

## ivec2 & operator+= ( int v )

Performs addition of the specified value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( int v )

Bitwise left shift by a specific value. Both components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftLeft ( const ivec2& v )

Bitwise left shift by a specific value. Both components are shifted by the value's corresponding component.
### Arguments

- *const ivec2&* **v** - Value.

## ivec2 & operator<<= ( const ivec2& v )

Bitwise left shift by a specific value. Both components are shifted by the value's corresponding component.
### Arguments

- *const ivec2&* **v** - Value.

### Return value

This vector.
## ivec2 & operator<<= ( int v )

Bitwise left shift by a specific value. Both components are shifted by this value.
### Arguments

- *int* **v** - Value.

### Return value

This vector.
## void shiftRight ( int v )

Bitwise right shift by a specific value. Both components are shifted by this value.
### Arguments

- *int* **v** - Value.

## void shiftRight ( const ivec2& v )

Bitwise right shift by a specific value. Both components are shifted by the value's corresponding component.
### Arguments

- *const ivec2&* **v** - Value.

## ivec2 & operator>>= ( const ivec2& v )

Bitwise right shift by a specific value. Both components are shifted by the value's corresponding component.
### Arguments

- *const ivec2&* **v** - Value.

### Return value

This vector.
## ivec2 & operator>>= ( int v )

Bitwise right shift by a specific value. Both components are shifted by this value.
### Arguments

- *int* **v** - Value.

### Return value

This vector.
## int max ( ) const

Returns the maximum of X and Y components.
## int min ( ) const

Returns the minimum of X and Y components.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
