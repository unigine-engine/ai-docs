# Unigine::UlonValue Class (CS)


This class is used to represent a [value](../../../api/library/common/class.ulonnode_cs.md) of a [ULON](../../../code/formats/ulon_format.md) node.


## UlonValue Class

### Properties

## 🔒︎ bool IsArray

The value indicating if the ULON node value is of an array type.
## bool Usage

The value indicating if the ULON node value is used (obtained via one of the *get*()* methods).
### Members

---

## UlonValue ( )

Constructor. Creates a ULON node value.
## UlonValue ( string arg1 )

Constructor. Creates a ULON node value from the specified source buffer.
### Arguments

- *string* **arg1** - ULON node value source buffer.

## string GetStr ( )

Returns the ULON node value as a non-formatted string.
### Return value

ULON node value as a non-formatted string.
## double GetDouble ( )

Returns the ULON node value as a double.
### Return value

Double ULON node value.
## float GetFloat ( )

Returns the ULON node value as a float.
### Return value

Float ULON node value.
## int GetInt ( )

Returns the ULON node value as an integer.
### Return value

Integer ULON node value.
## long GetLong ( )

Returns the ULON node value as a 64-bit long.
### Return value

64-bit long ULON node value.
## short GetShort ( )

### Return value

16-bit short ULON node value.
## byte GetChar ( )

Returns the ULON node value as a char.
### Return value

Char ULON node value.
## bool GetBool ( )

Returns the ULON node value as a boolean.
### Return value

Boolean ULON node value.
## string[] GetArray ( )

Returns the ULON node value as an array of strings.
### Return value

Array of strings representing elements of the array.
## dvec4 GetDVec4 ( )

Returns the ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cs.md) vector.
### Return value

ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cs.md) vector.
## vec4 GetVec4 ( )

Returns the ULON node value as a [vec4](../../../api/library/math/class.vec4_cs.md) vector.
### Return value

ULON node value as a [vec4](../../../api/library/math/class.vec4_cs.md) vector.
## ivec4 GetIVec4 ( )

Returns the ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cs.md) vector.
### Return value

ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cs.md) vector.
## void get ( out dvec4 ret )

Gets the ULON node value as a [dvec4](../../../api/library/math/class.dvec4_cs.md) and puts it to the specified output vector.
### Arguments

- *out dvec4* **ret** - Output [dvec4](../../../api/library/math/class.dvec4_cs.md) vector.

## void get ( out vec4 ret )

Gets the ULON node value as a [vec4](../../../api/library/math/class.vec4_cs.md) and puts it to the specified output vector.
### Arguments

- *out vec4* **ret** - Output [vec4](../../../api/library/math/class.vec4_cs.md) vector.

## void get ( out ivec4 ret )

Gets the ULON node value as an [ivec4](../../../api/library/math/class.ivec4_cs.md) and puts it to the specified output vector.
### Arguments

- *out ivec4* **ret** - Output [ivec4](../../../api/library/math/class.ivec4_cs.md) vector.

## int Read ( string src )

Reads the ULON node value from the specified source buffer.
### Arguments

- *string* **src** - ULON node value source buffer.
