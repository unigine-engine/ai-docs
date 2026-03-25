# Unigine::Plugins::DataBridge::DBVariable Class (CPP)

**Header:** #include <plugins/Unigine/DataBridge/UnigineDataBridge.h>


This class provides access to the variable and its methods.


## DBVariable Class

### Enums

## Type

| Name | Description |
|---|---|
| **Empty** = 0 | Empty value. |
| **Bool** = 1 | Boolean value. |
| **Int32** = 2 | Integer value. |
| **UInt32** = 3 | Unsigned integer value. |
| **Float32** = 4 | Floating point value. |
| **Float64** = 5 | Double value. |
| **Int64** = 6 | Long long value. |
| **UInt64** = 7 | Unsigned long long value. |
| **String** = 8 | String value. |
| **Blob** = 9 | Blob value. |
| **Directory** = 10 | Directory. This variable hasn't value of its own and stores other variables. |

### Members

## String getName () const

Returns the current variable name.
### Return value

Current variable name.
## String getPath () const

Returns the current path to the variable.
### Return value

Current path to the variable.
## unsigned long long getID () const

Returns the current variable ID.
### Return value

Current variable ID.
---

## void setEmpty ( )

Sets an empty value.
## void setBool ( bool val )

Sets a boolean value.
### Arguments

- *bool* **val** - Boolean value.

## void setInt32 ( int val )

Sets an integer value.
### Arguments

- *int* **val** - Integer value.

## void setUInt32 ( unsigned int val )

Sets an unsigned integer value.
### Arguments

- *unsigned int* **val** - Unsigned integer value.

## void setInt64 ( long long val )

Sets a long long value.
### Arguments

- *long long* **val** - Long long value.

## void setUInt64 ( unsigned long long val )

Sets an unsigned long long value.
### Arguments

- *unsigned long long* **val** - Unsigned long long value.

## void setFloat32 ( float val )

Sets a floating point value.
### Arguments

- *float* **val** - Floating point value.

## void setFloat64 ( double val )

Sets a double value.
### Arguments

- *double* **val** - Double value.

## void setString ( const char * val )

Sets a string value.
### Arguments

- *const char ** **val** - String value.

## void setBlob ( Ptr < Blob > & val )

Sets a blob value.
### Arguments

- *[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **val** - Blob value.

## bool getBool ( )

Returns a boolean value.
### Return value

Boolean value.
## int getInt32 ( )

Returns an integer value.
### Return value

Integer value.
## unsigned int getUInt32 ( )

Returns an unsigned integer value value.
### Return value

Unsigned integer value.
## float getFloat32 ( )

Returns a floating point value.
### Return value

Floating point value.
## double getFloat64 ( )

Returns a double value.
### Return value

Double value.
## long long getInt64 ( )

Returns a long long value.
### Return value

Long long value.
## unsigned long long getUInt64 ( )

Returns an unsigned long long value.
### Return value

Unsigned long long value.
## String getString ( )

Returns a string value.
### Return value

String value.
## Ptr < Blob > getBlob ( )

Returns a blob value.
### Return value

Blob value.
## int findChild ( const char * child_name ) const

Returns the number of the child variable with the specified name.
### Arguments

- *const char ** **child_name** - Name of the child variable to be found.

### Return value

Number of the child variable with the specified name, if it exists; otherwise, -1.
## int getNumChildren ( ) const

Returns the total number of children of the variable.
### Return value

Total number of children of the variable.
## DBVariable * addChild ( const char * child_name ) const

Returns the variable added as a child.
### Arguments

- *const char ** **child_name** - Name of the child variable to be added.

### Return value

Variable added as a child.
## DBVariable * getChild ( int index ) const

Returns a child variable by its number.
### Arguments

- *int* **index** - Number of the child variable in the range from 0 to the [total number of children](#getNumChildren_int) of this variable.

### Return value

Child variable smart pointer.
## DBVariable * getChild ( const char * child_name ) const

Returns a child variable by its name.
### Arguments

- *const char ** **child_name** - Child variable name.

### Return value

Child variable smart pointer, if it exists; otherwise, nullptr.
## bool isDirty ( ) const

Returns the value indicating if the variable has been changed since it was obtained.
### Return value

true if the variable has been changed since it was obtained, otherwise false.
## void clearDirtyState ( )

Clears the information that the variable has been changed after being obtained.
## void markDirty ( )

Sets the value indicating that the variable has been changed after it was obtained.
## bool isEmpty ( ) const

Returns the value indicating if the variable is empty.
### Return value

true if the variable has is empty, otherwise false.
## bool isDirectory ( ) const

Returns the value indicating if the variable is a directory.
### Return value

true if the variable is a directory, otherwise false.
## void saveState ( const Ptr < Stream > & stream )

Saves the state of the variable into a binary stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - The stream to save the variable data.

## void restoreState ( const Ptr < Stream > & stream )

Restores the state of the variable from the binary stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - The stream that stores the variable data.

## DBVariable::Type getType ( ) const

Returns the type of the variable, one of the [Type](#Type) values.
### Return value

type of the variable.
## String getValueString ( ) const

Returns the value of the variable as a string.
### Return value

Variable in the string format.
## bool isDeleted ( ) const

Returns the value indicating if the variable is deleted.
### Return value

true if the variable is deleted, otherwise false.
