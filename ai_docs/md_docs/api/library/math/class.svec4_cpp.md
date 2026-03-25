# Unigine::Math::svec4 Struct (CPP)

**Header:** #include <UnigineMathLibSVec4.h>


This class represents a vector with 4 unsigned short components.


## svec4 Struct

### Members

---

## svec4 ( )

Default constructor. Produces a zero vector.
## svec4 ( const svec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const svec4&* **v** - Source vector.

## svec4 ( unsigned short x , unsigned short y , unsigned short z , unsigned short w )

Constructor. Initializes the vector using given unsigned short values.
### Arguments

- *unsigned short* **x** - X component of the vector.
- *unsigned short* **y** - Y component of the vector.
- *unsigned short* **z** - Z component of the vector.
- *unsigned short* **w** - W component of the vector.

## svec4 ( const vec4& v , float scale )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector and a scale multiplier.
### Arguments

- *const vec4&* **v** - Source vector.
- *float* **scale** - Scale.

## explicit svec4 ( unsigned short v )

Constructor. Initializes the vector using a given value: x=v, y=v, z=v, w=v.
### Arguments

- *unsigned short* **v** - Source value.

## explicit svec4 ( const unsigned short* v )

Constructor. Initializes the vector using a given pointer to the array of unsigned short elements: x=v[0], y=v[1], z=v[2], w=v[3].
### Arguments

- *const unsigned short** **v** - Pointer to the array of unsigned short elements.

## explicit svec4 ( const dvec4& v )

Constructor. Initializes the vector using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## explicit svec4 ( const ivec4& v )

Constructor. Initializes the vector using a given [ivec4](../../../api/library/math/class.ivec4_cpp.md) source vector.
### Arguments

- *const ivec4&* **v** - Source vector.

## explicit svec4 ( const vec4& v )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## void set ( unsigned short val )

Sets the vector components equal to specified value: x=val, y=val, z=val, w=val.
### Arguments

- *unsigned short* **val** - Value.

## void set ( unsigned short x_ , unsigned short y_ , unsigned short z_ , unsigned short w_ )

Sets the vector by components.
### Arguments

- *unsigned short* **x_** - X component of the vector.
- *unsigned short* **y_** - Y component of the vector.
- *unsigned short* **z_** - Z component of the vector.
- *unsigned short* **w_** - W component of the vector.

## void set ( const svec4& val )

Sets the vector equal to the specified vector.
### Arguments

- *const svec4&* **val** - Source vector.

## void set ( const unsigned short* val )

Sets the vector using the array of unsigned short elements: x=val[0], y=val[1], z=val[2], w=val[3].
### Arguments

- *const unsigned short** **val** - Pointer to the array of unsigned short elements.

## void set ( const vec4& val , float scale )

Sets the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) vector and a scale multiplier.
### Arguments

- *const vec4&* **val** - Source vector.
- *float* **scale** - Scale.

## unsigned short * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const unsigned short * get ( ) const

Returns the constant pointer to the vector.
### Return value

Pointer to the vector.
## void get ( unsigned short* val ) const

Sets the array of unsigned short values equal to the vector.
### Arguments

- *unsigned short** **val** - The vector to be set.

## svec4 & operator= ( const svec4& val )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const svec4&* **val** - Source vector.

### Return value

Result.
## const unsigned short * operator const unsigned short * ( ) const

Performs type conversion to const unsigned short *.
## void * operator void * ( )

Performs type conversion to void *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## unsigned short * operator unsigned short * ( )

Performs type conversion to unsigned short *.
## unsigned short operator[] ( int i ) const

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## unsigned short & operator[] ( int i )

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
