# Unigine::Math::hvec2 Struct (CPP)

**Header:** #include <UnigineMathLibHVec2.h>


This class represents a vector of 2 [half](../../../api/library/math/class.half_cpp.md) (16-bit float) components.


## hvec2 Struct

### Members

---

## hvec2 ( )

Default constructor. Produces a zero vector.
## hvec2 ( const hvec2& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const hvec2&* **v** - Source vector.

## hvec2 ( half x , half y )

Constructor. Initializes the vector using given [half](../../../api/library/math/class.half_cpp.md) values.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **x** - X component of the vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **y** - Y component of the vector.

### Examples


```cpp
hvec2(2.0, 3.0);
/*
Creates a vector (2.0, 3.0)
*/

```


## hvec2 ( half v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Scalar value.

## hvec2 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v.
### Arguments

- *float* **v** - Scalar value.

## hvec2 ( const vec2& v )

Constructor. Initializes the vector using a given [vec2](../../../api/library/math/class.vec2_cpp.md) source vector.
### Arguments

- *const vec2&* **v** - Source vector.

## hvec2 ( const dvec2& v )

Constructor. Initializes the vector using a given [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector.
### Arguments

- *const dvec2&* **v** - Vector.

## const half * operator const Unigine::Math::half * ( ) const

Performs type conversion to const half *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## half * operator Unigine::Math::half * ( )

Performs type conversion to half *.
## void * operator void * ( )

Performs type conversion to void *.
## hvec2 & operator= ( const hvec2& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const hvec2&* **v** - Source vector.

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
