# Unigine::Math::hvec4 Struct (CPP)

**Header:** #include <UnigineMathLibHVec4.h>


This class represents a vector of 4 [half](../../../api/library/math/class.half_cpp.md) (16-bit float) components.


## hvec4 Struct

### Members

---

## hvec4 ( )

Default constructor. Produces a zero vector.
## hvec4 ( const hvec4& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const hvec4&* **v** - Source vector.

## hvec4 ( half x , half y , half z , half w )

Constructor. Initializes the vector using given [half](../../../api/library/math/class.half_cpp.md) values.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **x** - X component of the vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **y** - Y component of the vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **z** - Z component of the vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **w** - W component of the vector.

### Examples


```cpp
hvec4(2.0, 3.0, 1.0, 4.0);
/*
Creates a vector (2.0, 3.0, 1.0, 4.0)
*/

```


## hvec4 ( half v )

Constructor. Initializes the vector using given [half](../../../api/library/math/class.half_cpp.md) value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Scalar value.

### Examples


```cpp
hvec4(1.0);
/*
Creates a vector (1.0, 1.0, 1.0, 1.0)
*/

```


## hvec4 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v, w=v.
### Arguments

- *float* **v** - Scalar value.

## hvec4 ( const vec4& v )

Constructor. Initializes the vector using a given [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Source vector.

## hvec4 ( const dvec4& v )

Constructor. Initializes the vector using a given [dvec4](../../../api/library/math/class.dvec4_cpp.md) source vector.
### Arguments

- *const dvec4&* **v** - Source vector.

## const half * operator const Unigine::Math::half * ( ) const

Performs type conversion to const half *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## half * operator Unigine::Math::half * ( )

Performs type conversion to half *.
## void * operator void * ( )

Performs type conversion to void *.
## hvec4 & operator= ( const hvec4& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const hvec4&* **v** - Source vector.

### Return value

Result.
## half & operator[] ( int i )

Performs array access to the vector item reference by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item reference.
## half operator[] ( int i ) const

Performs array access to the vector item by using given item index.
### Arguments

- *int* **i** - Vector item index.

### Return value

Vector item.
## half * get ( )

Returns the X component of the vector.
### Return value

X component of the vector.
## const half * get ( ) const

Returns the X component of the vector a constant.
### Return value

X component of the vector.
