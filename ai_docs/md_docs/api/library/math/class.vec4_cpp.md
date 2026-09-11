# Unigine::Math::vec4 Struct (CPP)

**Header:** #include <UnigineMathLibVec4.h>


This class represents a vector of 4 float components.


## vec4 Struct

### Members

---

## vec4 ( const __m128& v )


Constructor. Initializes the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128&* **v** - 128-bit variable

## vec4 ( const quat& q )

Constructor. Initializes the vector using a given source [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const quat&* **q**

## vec4 ( const hvec4& v )

Constructor. Initializes the vector using a given [hvec4](../../../api/library/math/class.hvec4_cpp.md) source vector.
### Arguments

- *const hvec4&* **v** - Source vector.

## vec4 ( )

Default constructor. Produces a zero vector.
## vec4 ( const vec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## vec4 ( const vec2& v , float z , float w )

Constructor. Initializes the vector using a given two-component [vec2](../../../api/library/math/class.vec2_cpp.md) source vector and two scalars.
### Arguments

- *const vec2&* **v** - Two-component source vector.
- *float* **z** - Z component of the vector.
- *float* **w** - W component of the vector.

## vec4 ( const vec3& v , float w )

Constructor. Initializes the vector using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) source vector and a scalar.
### Arguments

- *const vec3&* **v** - Three-component source vector.
- *float* **w** - W component of the vector.

## vec4 ( float x , float y , float z , float w )

Constructor. Initializes the vector using given float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.
- *float* **z** - Z component of the vector.
- *float* **w** - W component of the vector.

## explicit vec4 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *float* **v** - Scalar value.

## explicit vec4 ( const vec2& v )

Constructor. Initializes the vector using a given two-component [vec2](../../../api/library/math/class.vec2_cpp.md) source vector: x=v.x, y=v.y, z=0.0f, w=1.0f.
### Arguments

- *const vec2&* **v** - Two-component source vector.

## explicit vec4 ( const vec3& v )

Constructor. Initializes the vector using a given three-component [vec3](../../../api/library/math/class.vec3_cpp.md) source vector: x=v.x, y=v.y, z=v.z, w=1.0f.
### Arguments

- *const vec3&* **v** - Three-component source vector.

## explicit vec4 ( const dvec4& v )

Constructor. Initializes the vector using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## explicit vec4 ( const ivec4& v )

Constructor. Initializes the vector using a given [ivec4](../../../api/library/math/class.ivec4_cpp.md) source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## explicit vec4 ( const bvec4& v )

Constructor. Initializes the vector using a given [bvec4](../../../api/library/math/class.bvec4_cpp.md) source vector.
### Arguments

- *const bvec4&* **v** - Source vector.

## explicit vec4 ( const svec4& v )

Constructor. Initializes the vector using a given [svec4](../../../api/library/math/class.svec4_cpp.md) source vector.
### Arguments

- *const svec4&* **v** - Source vector.

## explicit vec4 ( const float* v )

Constructor. Initializes the vector using a given pointer to the array of float elements: x=v[0], y=v[1], z=v[2], w=v[3].
### Arguments

- *const float** **v** - Pointer to the array of float elements.

## vec4 ( const dvec2& v0 , const dvec2& v1 )

Constructor. Initializes the vector using given two [dvec2](../../../api/library/math/class.dvec2_cpp.md) source vectors.
### Arguments

- *const dvec2&* **v0** - Two-component source vector.
- *const dvec2&* **v1** - Two-component source vector.

## vec4 ( const vec2& v0 , const vec2& v1 )

Constructor. Initializes the vector using given two [vec2](../../../api/library/math/class.vec2_cpp.md) source vectors.
### Arguments

- *const vec2&* **v0** - Two-component source vector.
- *const vec2&* **v1** - Two-component source vector.

## vec4 ( float x , float y , float z , float w , ConstexprTag )

Constructor. Initializes the vector using given float values.
### Arguments

- *float* **x** - X component of the vector.
- *float* **y** - Y component of the vector.
- *float* **z** - Z component of the vector.
- *float* **w** - W component of the vector.
- *ConstexprTag*  - Auxiliary tag.

## vec4 ( float v , ConstexprTag )

Constructor. Initializes the vector using a given *constant* scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *float* **v** - Constant scalar value.
- *ConstexprTag*  - Auxiliary tag.

## vec4 & abs ( )

Returns the absolute values of the vector components.
### Return value

Vector with absolute values.
## void set ( float x_ , float y_ , float z_ , float w_ )

Sets the vector by components.
### Arguments

- *float* **x_** - X component of the vector.
- *float* **y_** - Y component of the vector.
- *float* **z_** - Z component of the vector.
- *float* **w_** - W component of the vector.

## void set ( const float* v )

Sets the vector using the array of float elements: x=val[0], y=val[1], z=val[2], w=val[3].
### Arguments

- *const float** **v** - Pointer to the array of float elements.

## void set ( const vec4& v )

Sets the vector equal to the specified source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## void set ( const vec2& v , float z_ , float w_ )

Sets the vector using a two-component [vec2](../../../api/library/math/class.vec2_cpp.md) source vector and two scalars.
### Arguments

- *const vec2&* **v** - Two-component source vector.
- *float* **z_** - Z component of the vector.
- *float* **w_** - W component of the vector.

## void set ( const vec3& v , float w_ )

Sets the vector using a three-component [vec3](../../../api/library/math/class.vec3_cpp.md) source vector and a scalar.
### Arguments

- *const vec3&* **v** - Three-component source vector.
- *float* **w_** - W component of the vector.

## void set ( const quat& q )

Sets the vector using a [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const quat&* **q** - Quaternion.

## void set ( float v )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *float* **v** - Scalar value.

## void get ( float* v ) const

Gets the vector: val[0]=x, val[1]=y, val[2]=z, val[3]=w.
### Arguments

- *float** **v** - Pointer to the array of float elements.

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
## float lengthFast ( ) const

Returns the fast-calculated length of the vector.
## float iLength ( ) const

Returns the inverted length of the vector.
## float iLengthFast ( ) const

Returns the fast-calculated inverted length of the vector.
## float maxXY ( ) const

Compares the X and Y components of the vector and returns the greater one.
### Return value

The greater out of the X and Y components of the vector.
## float maxXYZ ( ) const

Compares the X, Y, and Z components of the vector and returns the greatest one.
### Return value

The greatest out of the X, Y, and Z vector components.
## float max ( ) const

Compares all components of the vector and returns the greatest value.
### Return value

The greatest out of the vector components.
## vec4 & normalize ( )

Returns a normalized vector.
### Return value

Normalized vector.
## vec4 & normalizeValid ( )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## vec4 & normalizeFast ( )

Returns a normalized vector, calculated using the fast inverse square root algorithm.
### Return value

Normalized vector.
## vec4 & normalizeValidFast ( )

Returns a normalized vector, calculated using the fast inverse square root algorithm. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Normalized vector.
## vec4 & normalize3 ( )

Returns the vector with normalized XYZ components.
### Return value

Vector with normalized XYZ components.
## vec4 & normalizeValid3 ( )

Returns the vector with normalized XYZ components. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Vector with normalized XYZ components.
## vec4 & normalizeFast3 ( )

Returns the vector with XYZ components normalized using the fast inverse square root algorithm.
### Return value

Vector with normalized XYZ components.
## vec4 & normalizeValidFast3 ( )

Returns the vector with XYZ components normalized using the fast inverse square root algorithm. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Return value

Vector with normalized XYZ components.
## const float * operator const float * ( ) const

Performs type conversion to const float *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## float * operator float * ( )

Performs type conversion to float *.
## void * operator void * ( )

Performs type conversion to void *.
## vec4 & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
## vec4 & operator*= ( const vec4& v )

Performs vector multiplication.
### Arguments

- *const vec4&* **v** - Vector.

### Return value

Resulting vector.
## vec4 & operator+= ( float v )

Performs addition of the specified value.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## vec4 & operator+= ( const vec4& v )

Performs vector addition.
### Arguments

- *const vec4&* **v** - Vector.

### Return value

Resulting vector.
## vec4 operator- ( ) const

Performs vector negation.
### Return value

Resulting vector.
## vec4 & operator-= ( const vec4& v )

Performs vector subtraction.
### Arguments

- *const vec4&* **v** - Vector.

### Return value

Resulting vector.
## vec4 & operator-= ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

### Return value

This vector.
## vec4 & operator/= ( float v )

Performs componentwise division of the vector by the scalar. Implemented using the calculation of inverse scalar value with subsequent by-component multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting vector.
## vec4 & operator/= ( const vec4& v )

Performs componentwise division of vectors.
### Arguments

- *const vec4&* **v** - Vector.

### Return value

Resulting vector.
## vec4 & operator= ( const __m128& v )


Sets the vector using a given 128-bit variable as a source.


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128&* **v** - 128-bit variable.

### Return value

Vector.
## vec4 & operator= ( const vec4& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const vec4&* **v** - Source vector.

### Return value

Result.
## vec4 & operator= ( const float v )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *const float* **v** - Scalar value.

### Return value

This vector.
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

## void mul ( const vec4& v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *const vec4&* **v** - Vector multiplier.

## void mul3 ( float v )

Multiplies the X, Y, and Z components of the vector by the value of the specified argument.
### Arguments

- *float* **v** - A *float* multiplier.

## void div ( float v )

Performs division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - A *float* divisor value.

## void div ( const vec4& v )

Performs division of the vector by the value of the specified arguments.
### Arguments

- *const vec4&* **v** - A *vec3* divisor value.

## float sum ( ) const

Returns the sum of vector components.
## void add ( float v )

Performs addition of the specified argument.
### Arguments

- *float* **v** - Value.

## void add ( const vec4& v )

Performs addition of the specified argument.
### Arguments

- *const vec4&* **v** - Value.

## void sub ( float v )

Subtracts the argument from all elements of the vector.
### Arguments

- *float* **v** - Value.

## void sub ( const vec4& v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *const vec4&* **v** - Value.

## static vec4 parseColor ( const char * str )

Converts a color string in the Web format (RRGGBB / #RRGGBB or RRGGBBAA / #RRGGBBAA) into its *vec4* equivalent.
### Arguments

- *const char ** **str** - Color string in the Web format.

### Return value

Color value as a *vec4* vector (R, G, B, A).
## unsigned int hash ( ) const

Returns a hash obtained by mixing the hash values of vector components.
### Return value

32-bit hash value.
## float rgbToLuma ( vec4 & color )

Returns the perceived brightness of the color.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

### Return value

Perceived brightness of the color.
