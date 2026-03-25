# Unigine::Plugins::DataBridge::DBVariable Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides access to the variable and its methods.


## DBVariable Class

### Members

## String getName () const

Returns the current variable name.
### Return value

Current variable name.
## String getPath () const

Returns the current path to the variable.
### Return value

Current path to the variable.
## long getID () const

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

## void setInt64 ( long val )

Sets a long long value.
### Arguments

- *long* **val** - Long long value.

## void setUInt64 ( long val )

Sets an unsigned long long value.
### Arguments

- *long* **val** - Unsigned long long value.

## void setFloat32 ( float val )

Sets a floating point value.
### Arguments

- *float* **val** - Floating point value.

## void setFloat64 ( double val )

Sets a double value.
### Arguments

- *double* **val** - Double value.

## void setString ( String val )

Sets a string value.
### Arguments

- *String* **val** - String value.

## void setBlob ( Blob & val )

Sets a blob value.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_usc.md) &* **val** - Blob value.

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
## long getInt64 ( )

Returns a long long value.
### Return value

Long long value.
## long getUInt64 ( )

Returns an unsigned long long value.
### Return value

Unsigned long long value.
## String getString ( )

Returns a string value.
### Return value

String value.
## Blob getBlob ( )

Returns a blob value.
### Return value

Blob value.
## int findChild ( string child_name )

Returns the number of the child variable with the specified name.
### Arguments

- *string* **child_name** - Name of the child variable to be found.

### Return value

Number of the child variable with the specified name, if it exists; otherwise, -1.
## int getNumChildren ( )

Returns the total number of children of the variable.
### Return value

Total number of children of the variable.
## DBVariable addChild ( string child_name )

Returns the variable added as a child.
### Arguments

- *string* **child_name** - Name of the child variable to be added.

### Return value

Variable added as a child.
## DBVariable getChild ( int index )

Returns a child variable by its number.
### Arguments

- *int* **index** - Number of the child variable in the range from 0 to the [total number of children](#getNumChildren_int) of this variable.

### Return value

Child variable instance.
## DBVariable getChild ( string child_name )

Returns a child variable by its name.
### Arguments

- *string* **child_name** - Child variable name.

### Return value

Child variable instance, if it exists; otherwise, NULL.
## bool isDirty ( )

Returns the value indicating if the variable has been changed since it was obtained.
### Return value

true if the variable has been changed since it was obtained, otherwise false.
## void clearDirtyState ( )

Clears the information that the variable has been changed after being obtained.
## void markDirty ( )

Sets the value indicating that the variable has been changed after it was obtained.
## bool isEmpty ( )

Returns the value indicating if the variable is empty.
### Return value

true if the variable has is empty, otherwise false.
## bool isDirectory ( )

Returns the value indicating if the variable is a directory.
### Return value

true if the variable is a directory, otherwise false.
## void saveState ( const Stream stream )

Saves the state of the variable into a binary stream.
### Arguments

- *const [Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - The stream to save the variable data.

## void restoreState ( const Stream stream )

Restores the state of the variable from the binary stream.
### Arguments

- *const [Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - The stream that stores the variable data.

## int getType ( )

Returns the type of the variable, one of the [Type](#Type) values.
### Return value

type of the variable.
## String getValueString ( )

Returns the value of the variable as a string.
### Return value

Variable in the string format.
## bool isDeleted ( )

Returns the value indicating if the variable is deleted.
### Return value

true if the variable is deleted, otherwise false.
