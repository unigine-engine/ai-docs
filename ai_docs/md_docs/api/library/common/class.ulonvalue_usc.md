# Unigine::UlonValue Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to represent a [value](../../../api/library/common/class.ulonnode_usc.md) of a [ULON](../../../code/formats/ulon_format.md) node.


## UlonValue Class

### Members

## int isArray () const

Returns the current value indicating if the ULON node value is of an array type.
### Return value

Current the ULON node value is of an array type
## void setUsage ( int usage )

Sets a new value indicating if the ULON node value is used (obtained via one of the *get*()* methods).
### Arguments

- *int* **usage** - The usage of the ULON node value

## int isUsage () const

Returns the current value indicating if the ULON node value is used (obtained via one of the *get*()* methods).
### Return value

Current usage of the ULON node value
---

## static UlonValue ( )

Constructor. Creates a ULON node value.
## static UlonValue ( string arg1 )

Constructor. Creates a ULON node value from the specified source buffer.
### Arguments

- *string* **arg1** - ULON node value source buffer.

## string getStr ( )

Returns the ULON node value as a non-formatted string.
### Return value

ULON node value as a non-formatted string.
## double getDouble ( )

Returns the ULON node value as a double.
### Return value

Double ULON node value.
## float getFloat ( )

Returns the ULON node value as a float.
### Return value

Float ULON node value.
## int getInt ( )

Returns the ULON node value as an integer.
### Return value

Integer ULON node value.
## long getLong ( )

Returns the ULON node value as a 64-bit long.
### Return value

64-bit long ULON node value.
## short getShort ( )

### Return value

16-bit short ULON node value.
## char getChar ( )

Returns the ULON node value as a char.
### Return value

Char ULON node value.
## bool getBool ( )

Returns the ULON node value as a boolean.
### Return value

Boolean ULON node value.
## Vector<String> getArray ( )

Returns the ULON node value as an array of strings.
### Return value

Array of strings representing elements of the array.
## dvec4 getDVec4 ( )

Returns the ULON node value as a [dvec4](../../../api/library/math/class.dvec4_usc.md) vector.
### Return value

ULON node value as a [dvec4](../../../api/library/math/class.dvec4_usc.md) vector.
## vec4 getVec4 ( )

Returns the ULON node value as a [vec4](../../../api/library/math/class.vec4_usc.md) vector.
### Return value

ULON node value as a [vec4](../../../api/library/math/class.vec4_usc.md) vector.
## ivec4 getIVec4 ( )

Returns the ULON node value as an [ivec4](../../../api/library/math/class.ivec4_usc.md) vector.
### Return value

ULON node value as an [ivec4](../../../api/library/math/class.ivec4_usc.md) vector.
## int read ( string src )

Reads the ULON node value from the specified source buffer.
### Arguments

- *string* **src** - ULON node value source buffer.
