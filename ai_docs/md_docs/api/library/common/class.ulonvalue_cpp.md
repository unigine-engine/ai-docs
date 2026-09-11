# Unigine::UlonValue Class (CPP)

**Header:** #include <UnigineUlon.h>


This class is used to represent a [value](../../../api/library/common/class.ulonnode_cpp.md) of a [ULON](../../../code/formats/ulon_format.md) node.


## UlonValue Class

### Members

## bool isArray () const

Returns the current value indicating if the ULON node value is of an array type.
### Return value

**true** if the ULON node value is of an array type; otherwise **false**.
## void setUsage ( bool usage )

Sets a new value indicating if the ULON node value is used (obtained via one of the *get*()* methods).
### Arguments

- *bool* **usage** - Set **true** to enable usage of the ULON node value; **false** - to disable it.

## bool isUsage () const

Returns the current value indicating if the ULON node value is used (obtained via one of the *get*()* methods).
### Return value

**true** if usage of the ULON node value is enabled ; otherwise **false**.
---

## static UlonValuePtr create ( )

Constructor. Creates a ULON node value.
## static UlonValuePtr create ( const char * arg1 )

Constructor. Creates a ULON node value from the specified source buffer.
### Arguments

- *const char ** **arg1** - ULON node value source buffer.

## const char * getStr ( ) const

Returns the ULON node value as a non-formatted string.
### Return value

ULON node value as a non-formatted string.
## double getDouble ( ) const

Returns the ULON node value as a double.
### Return value

Double ULON node value.
## float getFloat ( ) const

Returns the ULON node value as a float.
### Return value

Float ULON node value.
## int getInt ( ) const

Returns the ULON node value as an integer.
### Return value

Integer ULON node value.
## long long getLong ( ) const

Returns the ULON node value as a 64-bit long long.
### Return value

64-bit long long ULON node value.
## short getShort ( ) const

Returns the ULON node value as a 16-bit short.
### Return value

## char getChar ( ) const

Returns the ULON node value as a char.
### Return value

Char ULON node value.
## bool getBool ( ) const

Returns the ULON node value as a boolean.
### Return value

Boolean ULON node value.
## Vector < String > getArray ( ) const

Returns the ULON node value as an array of strings.
### Return value

Array of strings representing elements of the array.
## Math:: dvec4 getDVec4 ( ) const

Returns the ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector.
### Return value

ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector.
## Math:: vec4 getVec4 ( ) const

Returns the ULON node value as a [vec4](../../../api/library/math/class.vec4_cpp.md) vector.
### Return value

ULON node value as a [vec4](../../../api/library/math/class.vec4_cpp.md) vector.
## Math:: ivec4 getIVec4 ( ) const

Returns the ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector.
### Return value

ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector.
## void get ( Math:: dvec4 & ret ) const

Gets the ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cpp.md) and puts it to the specified output vector.
### Arguments

- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - Output [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector.

## void get ( Math:: vec4 & ret ) const

Gets the ULON node value as a [vec4](../../../api/library/math/class.vec4_cpp.md) and puts it to the specified output vector.
### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - Output [vec4](../../../api/library/math/class.vec4_cpp.md) vector.

## void get ( Math:: ivec4 & ret ) const

Gets the ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cpp.md) and puts it to the specified output vector.
### Arguments

- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **ret** - Output [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector.

## int read ( const char * src )

Reads the ULON node value from the specified source buffer.
### Arguments

- *const char ** **src** - ULON node value source buffer.
