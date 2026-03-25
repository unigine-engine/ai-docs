# Unigine::Plugins::DataBridge::DBVariable Class (CS)


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

### Properties

## 🔒︎ string Name

The variable name.
## 🔒︎ string Path

The path to the variable.
## 🔒︎ ulong ID

The variable ID.
### Members

---

## void SetEmpty ( )

Sets an empty value.
## void SetBool ( bool val )

Sets a boolean value.
### Arguments

- *bool* **val** - Boolean value.

## void SetInt32 ( int val )

Sets an integer value.
### Arguments

- *int* **val** - Integer value.

## void SetUInt32 ( uint val )

Sets an unsigned integer value.
### Arguments

- *uint* **val** - Unsigned integer value.

## void SetInt64 ( long val )

Sets a long long value.
### Arguments

- *long* **val** - Long long value.

## void SetUInt64 ( ulong val )

Sets an unsigned long long value.
### Arguments

- *ulong* **val** - Unsigned long long value.

## void SetFloat32 ( float val )

Sets a floating point value.
### Arguments

- *float* **val** - Floating point value.

## void SetFloat64 ( double val )

Sets a double value.
### Arguments

- *double* **val** - Double value.

## void SetString ( string val )

Sets a string value.
### Arguments

- *string* **val** - String value.

## void SetBlob ( Blob val )

Sets a blob value.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **val** - Blob value.

## bool GetBool ( )

Returns a boolean value.
### Return value

Boolean value.
## int GetInt32 ( )

Returns an integer value.
### Return value

Integer value.
## uint GetUInt32 ( )

Returns an unsigned integer value value.
### Return value

Unsigned integer value.
## float GetFloat32 ( )

Returns a floating point value.
### Return value

Floating point value.
## double GetFloat64 ( )

Returns a double value.
### Return value

Double value.
## long GetInt64 ( )

Returns a long long value.
### Return value

Long long value.
## ulong GetUInt64 ( )

Returns an unsigned long long value.
### Return value

Unsigned long long value.
## string GetString ( )

Returns a string value.
### Return value

String value.
## Blob GetBlob ( )

Returns a blob value.
### Return value

Blob value.
## int FindChild ( string child_name )

Returns the number of the child variable with the specified name.
### Arguments

- *string* **child_name** - Name of the child variable to be found.

### Return value

Number of the child variable with the specified name, if it exists; otherwise, -1.
## int GetNumChildren ( )

Returns the total number of children of the variable.
### Return value

Total number of children of the variable.
## DBVariable AddChild ( string child_name )

Returns the variable added as a child.
### Arguments

- *string* **child_name** - Name of the child variable to be added.

### Return value

Variable added as a child.
## DBVariable GetChild ( int index )

Returns a child variable by its number.
### Arguments

- *int* **index** - Number of the child variable in the range from 0 to the [total number of children](#getNumChildren_int) of this variable.

### Return value

Child variable instance.
## DBVariable GetChild ( string child_name )

Returns a child variable by its name.
### Arguments

- *string* **child_name** - Child variable name.

### Return value

Child variable instance, if it exists; otherwise, NULL.
## bool IsDirty ( )

Returns the value indicating if the variable has been changed since it was obtained.
### Return value

true if the variable has been changed since it was obtained, otherwise false.
## void ClearDirtyState ( )

Clears the information that the variable has been changed after being obtained.
## void MarkDirty ( )

Sets the value indicating that the variable has been changed after it was obtained.
## bool IsEmpty ( )

Returns the value indicating if the variable is empty.
### Return value

true if the variable has is empty, otherwise false.
## bool IsDirectory ( )

Returns the value indicating if the variable is a directory.
### Return value

true if the variable is a directory, otherwise false.
## void SaveState ( Stream stream )

Saves the state of the variable into a binary stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - The stream to save the variable data.

## void RestoreState ( Stream stream )

Restores the state of the variable from the binary stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - The stream that stores the variable data.

## DBVariable.Type GetType ( )

Returns the type of the variable, one of the [Type](#Type) values.
### Return value

type of the variable.
## string GetValueString ( )

Returns the value of the variable as a string.
### Return value

Variable in the string format.
## bool IsDeleted ( )

Returns the value indicating if the variable is deleted.
### Return value

true if the variable is deleted, otherwise false.
