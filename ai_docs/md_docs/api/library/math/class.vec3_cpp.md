# Unigine::Math::vec3 Struct (CPP)

**Header:** #include <UnigineMathLibVec3.h>


This class represents a vector of 3 float components.


## vec3 Struct

### Members

---

## vec3 ( const __m128& v )


Constructor. Initializes the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128&* **v** - 128-bit variable

## vec3 ( const hvec3& v )

Constructor. Initializes the vector using a given [hvec3](../../../api/library/math/class.hvec3_cpp.md) source vector.
### Arguments

- *const hvec3&* **v** - Source vector.

## vec3 ( )

Default constructor. Produces a zero vector.
## vec3 ( const vec3& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const vec3&* **v** - Source vector.

## vec3 ( const vec2& v , float z )

Constructor. Initializes the vector using a given two-component [vec2](../../../api/library/math/class.vec2_cpp.md) source vector and a scalar.
### Arguments

- *const vec2&* **v** - Two-component vector.
- *float* **z** - Z component of the vector.

## vec3 ( float x , float y , float z )

Constructor. Initializes the vector using given float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.
- *float* **z** - Z component of the vector.

## explicit vec3 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *float* **v** - Scalar value.

### Examples


```cpp
vec3(1.0);
/*
Creates a vector (1.0, 1.0, 1.0)
*/

```


## explicit vec3 ( const vec2& v )

Constructor. Initializes the vector using a given [vec2](../../../api/library/math/class.vec2_cpp.md) source vector: x=v.x, y=v.y, z=0.0f.
### Arguments

- *const vec2&* **v** - Two-component source vector.

## explicit vec3 ( const vec4& v )

Constructor. Initializes the vector using a given four-component [vec4](../../../api/library/math/class.vec4_cpp.md) source vector: x=v.x, y=v.y, z=v.z.
### Arguments

- *const vec4&* **v** - Four-component source vector.

## explicit vec3 ( const dvec3& v )

Constructor. Initializes the vector using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.
### Arguments

- *const dvec3&* **v** - Source vector.

## explicit vec3 ( const ivec3& v )

Constructor. Initializes the vector using a given [ivec3](../../../api/library/math/class.ivec3_cpp.md) source vector .
### Arguments

- *const ivec3&* **v** - Source vector.

## explicit vec3 ( const float* v )

Constructor. Initializes the vector using a given pointer to the array of float elements: x=v[0], y=v[1], z=v[2].
### Arguments

- *const float** **v** - Pointer to the array of float elements.

## vec3 ( float x , float y , float z , ConstexprTag )

Constructor. Initializes the vector using given *constant* float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.
- *float* **z** - Z component of the vector.
- *ConstexprTag*  - Auxiliary tag.

## vec3 ( float v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v, z=v.
### Arguments

- *float* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## vec3 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( float x_ , float y_ , float z_ )

Sets the vector by components.
### Arguments

- *float* **x_** - X component of the vector.
- *float* **y_** - Y component of the vector.
- *float* **z_** - Z component of the vector.

## void set ( const float* val )

Sets the vector using the array of float elements: x=val[0], y=val[1], z=val[2].
### Arguments

- *const float** **val** - Pointer to the array of float elements.

## void set ( const vec4& v )

Sets the vector using a [vec4](../../../api/library/math/class.vec4_cpp.md) source vector: x=v.x, y=v.y, z=v.z.
### Arguments

- *const vec4&* **v** - Source vector.

## void set ( const vec2& val , float z_ )

Sets the vector using a two-component [vec2](../../../api/library/math/class.vec2_cpp.md) source vector and a scalar.
### Arguments

- *const vec2&* **val** - Two-component source vector.
- *float* **z_** - Scalar.

## void set ( const vec3& val )

Sets the vector equal to the specified source vector.
### Arguments

- *const vec3&* **val** - Source vector.

## void set ( float val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val.
### Arguments

- *float* **val** - Scalar.

## void get ( float* val ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z.
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
## float maxXY ( ) const

Compares the X and Y components of the vector and returns the greater one.
### Return value

The greater out of the X and Y components of the vector.
## float max ( ) const

Compares all vector components and returns the maximum value.
### Return value

The greatest out of the vector components.
## float minXY ( )

Compares the X and Y components of the vector and returns the lower one.
### Return value

The lower value out of the X and Y components of the vector.
## vec3 & normalize ( )

Returns normalized vector.
### Return value

Normalized vector.
## vec3 & normalizeValid ( )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## vec3 & normalizeFast ( )

Returns normalized vector, calculated using the fast inverse square root algorithm.
### Return value

Normalized vector.
## vec3 & normalizeValidFast ( )

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
## vec3 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
## vec3 & operator*= ( const vec3& v )

Performs vector multiplication.
### Arguments

- *const vec3&* **v** - Vector.

### Return value

Resulting vector.
## vec3 & operator+= ( const vec3& v )

Performs vector addition.
### Arguments

- *const vec3&* **v** - Vector.

### Return value

Resulting vector.
## vec3 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## vec3 & operator-= ( const vec3& v )

Performs vector subtraction.
### Arguments

- *const vec3&* **v** - Vector.

### Return value

Resulting vector.
## vec3 & operator/= ( const vec3& v )

Performs componentwise division of vectors.
### Arguments

- *const vec3&* **v** - Vector.

### Return value

Resulting vector.
### Examples


```cpp
vec3 a, b;
a = vec3(6.0, 10.0, 12.0);
b = vec3(2.0, 5.0, 6.0);
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


## vec3 & operator/= ( float v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
### Examples


```cpp
vec3 a = vec3(6.0, 10.0, 12.0);
a /= 2.0;
/*
Initial value of vector a:
	a (6.0, 10.0, 12.0)

	a /= 2.0;
Vector a after operation:
	a (3.0, 5.0, 6.0)
*/

```


## vec3 & operator= ( const vec3& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const vec3&* **v** - Source vector.

### Return value

Result.
## vec3 & operator= ( const __m128& val )


Sets the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128&* **val** - 128-bit variable.

### Return value

Vector.
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

## void mul ( const vec3& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const vec3&* **v** - Vector multiplier.

## void div ( float v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - A *float* divisor value.

## void div ( const vec3& v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *const vec3&* **v** - A *vec3* divisor value.

## float sum ( ) const

Returns the sum of vector components.
## void add ( float v )

Performs addition of the specified argument.
### Arguments

- *float* **v** - Value.

## void add ( const vec3& v )

Performs addition of the specified argument.
### Arguments

- *const vec3&* **v** - Value.

## vec3 & operator+= ( float v )

Performs addition of the specified value.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## void sub ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

## void sub ( const vec3& v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *const vec3&* **v** - Value.

## vec3 & operator-= ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## float lengthFast ( ) const

Returns the length of the vector (fast version).
## float iLength ( ) const

Returns the inverted length of the vector.
## float iLengthFast ( ) const

Returns the inverted length of the vector (fast version).
## float min ( )

Returns the minimum value among all components.
## vec3 sign ( )

Returns the vector with signs of the argument components.
### Return value

Vector with signs of the argument components. **1.0** if *v* >= **0.0** ; **-1.0** if *v* < **0.0**.
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
## vec3 & reflect ( vec3 & ret , const vec3 & v0 , const vec3 & v1 )

Computes the reflection of a vector (v0) about another vector (v1) and stores the result in the ret value.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Vector to store the returned value.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Vector to be reflected.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Vector to reflect about.

### Return value

Reflected vector.
## vec3 & reflect ( const vec3 & v0 , const vec3 & v1 )

Computes the reflection of a vector (v0) about another vector (v1) and stores the result in the ret value.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Vector to be reflected.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Vector to reflect about.

### Return value

Reflected vector.
## bool areCollinear ( const vec3 & v0 , const vec3 & v1 )

Checks if the vectors are collinear.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

true if the vectors are collinear; otherwise, false.
