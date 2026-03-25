# Unigine::Math::bvec4 Struct (CPP)

**Header:** #include <UnigineMathLibBVec4.h>


This class represents a vector of 4 byte (unsigned char) components. This vector is used for vertex color parameters.


## bvec4 Struct

### Members

---

## bvec4 ( )

Default constructor. Produces a zero vector.
## explicit bvec4 ( unsigned char v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *unsigned char* **v** - Scalar.

## bvec4 ( unsigned char x , unsigned char y , unsigned char z , unsigned char w )

Constructor. Initializes the vector using given unsigned char values.
### Arguments

- *unsigned char* **x** - X component of the vector.
- *unsigned char* **y** - Y component of the vector.
- *unsigned char* **z** - Z component of the vector.
- *unsigned char* **w** - W component of the vector.

## explicit bvec4 ( const unsigned char* v )

Constructor. Initializes the vector using a given pointer to the array of unsigned char elements: x=v[0], y=v[1], z=v[2], w=v[3].
### Arguments

- *const unsigned char** **v** - Pointer to the array of unsigned char elements.

## bvec4 ( const bvec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const bvec4&* **v** - Source vector.

## explicit bvec4 ( const vec4& v )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## explicit bvec4 ( const dvec4& v )

Constructor. Initializes the vector using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## explicit bvec4 ( const ivec4& v )

Constructor. Initializes the vector using a given [ivec4](../../../api/library/math/class.ivec4_cpp.md) source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## bvec4 ( const vec4& v , float scale )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector and a scale multiplier.
### Arguments

- *const vec4&* **v** - Source vector.
- *float* **scale** - Scale.

## void set ( unsigned char x_ , unsigned char y_ , unsigned char z_ , unsigned char w_ )

Sets the vector by components.
### Arguments

- *unsigned char* **x_** - X component of the vector.
- *unsigned char* **y_** - Y component of the vector.
- *unsigned char* **z_** - Z component of the vector.
- *unsigned char* **w_** - W component of the vector.

## void set ( const unsigned char* val )

Sets the vector using the array of unsigned char elements: x=val[0], y=val[1], z=val[2], w=val[3].
### Arguments

- *const unsigned char** **val** - Pointer to the array of unsigned char elements.

## void set ( unsigned char val )

Sets the vector components equal to specified scalar value: x=val, y=val, z=val, w=val.
### Arguments

- *unsigned char* **val** - Scalar value.

## void set ( const bvec4& val )

Sets the vector equal to the specified vector.
### Arguments

- *const bvec4&* **val** - Source vector.

## void set ( const vec4& val , float scale )

Sets the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) vector and a scale multiplier.
### Arguments

- *const vec4&* **val** - Source vector.
- *float* **scale** - Scale.

## unsigned char * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const unsigned char * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## void get ( unsigned char* val ) const

Returns the vector by saving it in the argument.
### Arguments

- *unsigned char** **val** - Pointer to the vector to store the obtained data.

## unsigned char * operator unsigned char * ( ) const

Performs type conversion to unsigned char *.
### Return value

Pointer to the value.
## const unsigned char * operator const unsigned char * ( ) const

Performs type conversion to const unsigned char *.
### Return value

Pointer to the value.
## void * operator void * ( )

Performs type conversion to void *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## unsigned char & operator[] ( int i )

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
## unsigned char operator[] ( int i ) const

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## bvec4 & operator= ( const bvec4 & val )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **val** - Source vector.

### Return value

Result.
## int compare ( const bvec4 & v0 , const bvec4 & v1 )

Performs equal comparison.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

**1** if the first vector equals the second one; otherwise **0**.
## int operator== ( const bvec4 & v0 , const bvec4 & v1 )

Performs equal comparison.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

**1** if the first vector equals the second one; otherwise **0**.
## int operator!= ( const bvec4 & v0 , const bvec4 & v1 )

Not equal comparison.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

**1** if the first vector is not equal the second one; otherwise **0**.
## bvec4 min ( const bvec4 & v0 , const bvec4 & v1 )

Creates a new minimum vector based on input.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

Vector where each component is the minimum of the original vectors' corresponding components.
## bvec4 max ( const bvec4 & v0 , const bvec4 & v1 )

Creates a new maximum vector based on input.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

Vector where each component is the maximum of the original vectors' corresponding components.
## bvec4 clamp ( const bvec4 & v , const bvec4 & v0 , const bvec4 & v1 )

Clamps the vector based on the lower and upper limit vectors.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v** - The vector to clamp.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - Lower clamping limit.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Upper clamping limit.

### Return value

Vector where each component of the original vector is clamped based on the limit range provided by the lower and upper vectors' corresponding components.
