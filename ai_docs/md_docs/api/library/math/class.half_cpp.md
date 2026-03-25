# Unigine::Math::half Struct (CPP)

**Header:** #include <UnigineMathLibCommon.h>


This class represents a half (16-bit) float type.


## half Class

### Members

---

## half ( )

Default constructor. Produces a zero value.
## half ( const half& h )

Constructor. Initializes the value using a given half value.
### Arguments

- *const half&* **h** - Half value.

## explicit half ( int i )

Constructor. Initializes the value using a given integer value.
### Arguments

- *int* **i** - Integer value.

## explicit half ( float f )

Constructor. Initializes the value using a given float value.
### Arguments

- *float* **f** - Float value.

## void setFloat ( float f )

Sets the value using a given float value.
### Arguments

- *float* **f** - Float value.

## float getFloat ( ) const

Returns the float value.
### Return value

Float value.
## float operator float ( ) const

Performs type conversion to float type.
### Return value

Float value.
## unsigned short operator unsigned short ( ) const

Performs type conversion to unsigned short.
## half & operator= ( half v )

Performs assignment operation. Destination = Source.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Source.

## half & operator= ( float f )

Performs assignment operation. Destination = Source.
### Arguments

- *float* **f** - Source.
