# Unigine::Math::hvec3 Struct (CPP)

**Header:** #include <UnigineMathLibHVec3.h>


This class represents a vector of 3 [half](../../../api/library/math/class.half_cpp.md) (16-bit float) components.

> **Warning:** Do not use the fourth component in the structure (*align*) as it may be implicitly changed by the structure�s operations.


## hvec3 Struct

### Members

---

## hvec3 ( )

Default constructor. Produces a zero vector.
## hvec3 ( const hvec3& v )

Constructor. Initializes the vector by copying a given source vector.
### Arguments

- *const hvec3&* **v** - Source vector.

## hvec3 ( half x , half y , half z )

Constructor. Initializes the vector using given [half](../../../api/library/math/class.half_cpp.md) values.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **x** - The first component of the hvec3 vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **y** - The second component of the hvec3 vector.
- *[half](../../../api/library/math/class.half_cpp.md)* **z** - The third component of the hvec3 vector.

### Examples


```cpp
hvec3(2.0, 3.0, 1.0);
/*
Creates a vector (2.0, 3.0, 1.0)
*/

```


## hvec3 ( half v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Scalar value.

### Examples


```cpp
hvec3(1.0);
/*
Creates a vector (1.0, 1.0, 1.0)
*/

```


## hvec3 ( float v )

Constructor. Initializes the vector using a given scalar value: x=v, y=v, z=v.
### Arguments

- *float* **v** - Scalar value.

### Examples


```cpp
hvec3(1.0);
/*
Creates a vector (1.0, 1.0, 1.0)
*/

```


## hvec3 ( const vec3& v )

Constructor. Initializes the vector using a given [vec3](../../../api/library/math/class.vec3_cpp.md) source vector.
### Arguments

- *const vec3&* **v** - Source vector.

## hvec3 ( const dvec3& v )

Constructor. Initializes the vector using a given [dvec3](../../../api/library/math/class.dvec3_cpp.md) source vector.
### Arguments

- *const dvec3&* **v** - Source vector.

## const half * operator const Unigine::Math::half * ( ) const

Performs type conversion to const half *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## half * operator Unigine::Math::half * ( )

Performs type conversion to half *.
## void * operator void * ( )

Performs type conversion to void *.
## hvec3 & operator= ( const hvec3& v )

Performs vector assignment. Destination vector = Source vector.
### Arguments

- *const hvec3&* **v** - Source vector.

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
