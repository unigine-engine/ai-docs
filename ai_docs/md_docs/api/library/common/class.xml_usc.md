# Unigine::Xml Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


As Unigine extensively uses XML for storing different types of data, it also provides functionality for parsing and saving files of this type.


### Example


The example below creates an Xml and prints all added data to the console.


### See Also


- C++ sample
- C# sample


## Xml Class

### Members

## void setQuatData ( quat data )

Sets a new quaternion interpretation of data stored in the node.
### Arguments

- *quat* **data** - The quaternion interpretation of data stored in the node.

## quat getQuatData () const

Returns the current quaternion interpretation of data stored in the node.
### Return value

Current quaternion interpretation of data stored in the node.
## void setDMat4Data ( dmat4 data )

Sets a new *dmat4* matrix interpretation of data stored in the node.
### Arguments

- *dmat4* **data** - The *dmat4* matrix interpretation of data stored in the node.

## dmat4 getDMat4Data () const

Returns the current *dmat4* matrix interpretation of data stored in the node.
### Return value

Current *dmat4* matrix interpretation of data stored in the node.
## void setMat4Data ( mat4 data )

Sets a new *mat4* matrix interpretation of data stored in the node.
### Arguments

- *mat4* **data** - The *mat4* matrix interpretation of data stored in the node.

## mat4 getMat4Data () const

Returns the current *mat4* matrix interpretation of data stored in the node.
### Return value

Current *mat4* matrix interpretation of data stored in the node.
## void setIVec4Data ( ivec4 data )

Sets a new *ivec4* interpretation of data stored in the node.
### Arguments

- *ivec4* **data** - The *ivec4* interpretation of data stored in the node.

## ivec4 getIVec4Data () const

Returns the current *ivec4* interpretation of data stored in the node.
### Return value

Current *ivec4* interpretation of data stored in the node.
## void setIVec3Data ( ivec3 data )

Sets a new *ivec3* interpretation of data stored in the node.
### Arguments

- *ivec3* **data** - The *ivec3* interpretation of data stored in the node.

## ivec3 getIVec3Data () const

Returns the current *ivec3* interpretation of data stored in the node.
### Return value

Current *ivec3* interpretation of data stored in the node.
## void setIVec2Data ( ivec2 data )

Sets a new *ivec2* interpretation of data stored in the node.
### Arguments

- *ivec2* **data** - The *ivec2* interpretation of data stored in the node.

## ivec2 getIVec2Data () const

Returns the current *ivec2* interpretation of data stored in the node.
### Return value

Current *ivec2* interpretation of data stored in the node.
## void setDVec4Data ( dvec4 data )

Sets a new *dvec4* interpretation of data stored in the node.
### Arguments

- *dvec4* **data** - The *dvec4* interpretation of data stored in the node.

## dvec4 getDVec4Data () const

Returns the current *dvec4* interpretation of data stored in the node.
### Return value

Current *dvec4* interpretation of data stored in the node.
## void setDVec3Data ( dvec3 data )

Sets a new *dvec3* interpretation of data stored in the node.
### Arguments

- *dvec3* **data** - The *dvec3* interpretation of data stored in the node.

## dvec3 getDVec3Data () const

Returns the current *dvec3* interpretation of data stored in the node.
### Return value

Current *dvec3* interpretation of data stored in the node.
## void setDVec2Data ( dvec2 data )

Sets a new *dvec2* interpretation of data stored in the node.
### Arguments

- *dvec2* **data** - The *dvec2* interpretation of data stored in the node.

## dvec2 getDVec2Data () const

Returns the current *dvec2* interpretation of data stored in the node.
### Return value

Current *dvec2* interpretation of data stored in the node.
## void setVec4Data ( vec4 data )

Sets a new *vec4* interpretation of data stored in the node.
### Arguments

- *vec4* **data** - The *vec4* interpretation of data stored in the node.

## vec4 getVec4Data () const

Returns the current *vec4* interpretation of data stored in the node.
### Return value

Current *vec4* interpretation of data stored in the node.
## void setVec3Data ( vec3 data )

Sets a new *vec3* interpretation of data stored in the node.
### Arguments

- *vec3* **data** - The *vec3* interpretation of data stored in the node.

## vec3 getVec3Data () const

Returns the current *vec3* interpretation of data stored in the node.
### Return value

Current *vec3* interpretation of data stored in the node.
## void setVec2Data ( vec2 data )

Sets a new *vec2* interpretation of data stored in the node.
### Arguments

- *vec2* **data** - The *vec2* interpretation of data stored in the node.

## vec2 getVec2Data () const

Returns the current *vec2* interpretation of data stored in the node.
### Return value

Current *vec2* interpretation of data stored in the node.
## void setDoubleData ( double data )

Sets a new *double* interpretation of data stored in the node.
### Arguments

- *double* **data** - The *double* interpretation of data stored in the node.

## double getDoubleData () const

Returns the current *double* interpretation of data stored in the node.
### Return value

Current *double* interpretation of data stored in the node.
## void setFloatData ( float data )

Sets a new *float* interpretation of data stored in the node.
### Arguments

- *float* **data** - The *float* interpretation of data stored in the node.

## float getFloatData () const

Returns the current *float* interpretation of data stored in the node.
### Return value

Current *float* interpretation of data stored in the node.
## void setLongData ( long data )

Sets a new *long* interpretation of data stored in the node.
### Arguments

- *long* **data** - The *long* interpretation of data stored in the node.

## long getLongData () const

Returns the current *long* interpretation of data stored in the node.
### Return value

Current *long* interpretation of data stored in the node.
## void setBoolData ( bool data )

Sets a new boolean interpretation of data stored in the node.
### Arguments

- *bool* **data** - Set **true** to enable the value equals to true; **false** - to disable it.

## bool getBoolData () const

Returns the current boolean interpretation of data stored in the node.
### Return value

**true** if the value equals to true; otherwise **false**.
## void setData ( )

Sets a new data from the XML file.
### Arguments

- **data** - The data from the XML file.

## const char * getData () const

Returns the current data from the XML file.
### Return value

Current data from the XML file.
## int getNumArgs () const

Returns the current number of arguments.
### Return value

Current number of arguments.
## int getNumChildren () const

Returns the current number of children contained in the node.
In the standard XML model the child nodes can be of the following types: node, text node and comment. The data of the XML node is considered to be an unnamed child node, resulting in correct parsing of such a code:


```xml
<text>
	text</br>text
</text>

```


Hence if a node has the data, it will add to the number of its children.


### Return value

Current
## void setName ( string name )

Sets a new name of the node.
### Arguments

- *string* **name** - The name of the node.

## const char * getName () const

Returns the current name of the node.
### Return value

Current name of the node.
## const char * getLoadPath () const

Returns the current path to an XML file from which the data of the XML instance was loaded.
### Return value

Current path to an XML file from which the data of the XML instance was loaded.
---

## static Xml ( )

Default constructor that creates an empty instance.
## static Xml ( string name , string args = 0 )

Creates an XML tree with a given node as a root.
### Arguments

- *string* **name** - Name of the node that will be a root.
- *string* **args** - Optional arguments to the root node. If provided, they should be in this form: *arg1=\"value1\" arg2=\"value2\" �* If values do not contain spaces, escaped quotes can be omitted.

## bool setArg ( )

Sets a literal value of a given argument.
### Arguments

### Return value

true if the argument is set successfully; otherwise, false.
## int isArg ( string name )

Checks whether an argument with a given name exists.
### Arguments

- *string* **name** - Name to check.

### Return value

**1** if the argument exists; otherwise, **0**.
## void setArgName ( int num , string name )

Sets the XML argument name.
### Arguments

- *int* **num** - The argument number.
- *string* **name** - The argument name.

## string getArgName ( int num )

Returns argument name by its number.
### Arguments

- *int* **num** - Argument number.

### Return value

Argument name.
## void setArgValue ( int num , string value )

Sets the XML argument value.
### Arguments

- *int* **num** - The argument number.
- *string* **value** - The argument value.

## string getArgValue ( int num )

Returns the XML argument value.
### Arguments

- *int* **num** - The argument number.

### Return value

Argument value.
## int setBoolArg ( string name , int value )

Sets a value of a given boolean argument.
### Arguments

- *string* **name** - Name of an argument.
- *int* **value** - Value of the argument. Any non-zero value means true, the zero value means false.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int getBoolArg ( string name , int value )


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *int* **value** - Default value of the argument.

### Return value

**1** if the argument has a value 1, true or TRUE; **0**, if the argument has a value 0, false or FALSE; otherwise, **0**.
## int getBoolArg ( string name )


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

**1** if the argument has a value of 1, **1** or TRUE; or **0**, if the argument has a value 0, **0** or FALSE; otherwise, 0.
## getChild ( int num )


Returns a child node by its name or index number in the child list.


> **Notice:** To check if a child with a given name exists, use the [*isChild()*](#isChild_cstr_int) method.


### Arguments

- *int* **num** - Name of a node ([*string*](../../../code/uniginescript/language/data_types.md#string)) or its index number in the child list ([*int*](../../../code/uniginescript/language/data_types.md#int)).

### Return value

Target child node, if it is found; otherwise, **0**.
## int isChild ( string name )

Checks if a child element with a given name exists.
### Arguments

- *string* **name** - Element name to check.

### Return value

**1** if a child with the provided name exists; otherwise, **0**.
## getChildData ( variable value )

Returns the data from the XML child node.
### Arguments

- *variable* **value** - Type of the child (*int, float, vec3, vec4, dvec3, dvec4, ivec3, ivec4, mat4, dmat4, quat, string*).

### Return value

The value of the child node.
## int setDMat4Arg ( string name , dmat4 value )

Sets a value of a given *dmat4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dmat4* **value** - Value of an argument.

### Return value

Always **1**.
## dmat4 getDMat4Arg ( string name )


Returns a value of a given *dmat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setDoubleArg ( string name , double value )

Sets a value of a given *double* argument.
### Arguments

- *string* **name** - Name of an argument.
- *double* **value** - Value of an argument.

### Return value

Always **1**.
## double getDoubleArg ( string name , double value )


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *double* **value** - Default value of the argument.

### Return value

Argument value.
## double getDoubleArg ( string name )


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setDVec2Arg ( string name , dvec2 value )

Sets a value of a given *dvec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec2* **value** - Value of an argument.

### Return value

Always **1**.
## dvec2 getDVec2Arg ( string name )

Returns a value of a given *dvec2* argument.
> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setDVec3Arg ( string name , dvec3 value )

Sets a value of a given *dvec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec3* **value** - Value of an argument.

### Return value

Always **1**.
## dvec3 getDVec3Arg ( string name )


Returns a value of a given *dvec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setDVec4Arg ( string name , dvec4 value )

Sets a value of a given *dvec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec4* **value** - Value of an argument.

### Return value

Always **1**.
## dvec4 getDVec4Arg ( string name )


Returns a value of a given *dvec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setFloatArg ( string name , float value )

Sets a value of a given *float* argument.
### Arguments

- *string* **name** - Name of an argument.
- *float* **value** - Value of an argument.

### Return value

Always **1**.
## float getFloatArg ( string name , float value )


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *float* **value** - Default value of the argument.

### Return value

Argument value.
## float getFloatArg ( string name )


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## getFormattedSubTree ( )

Converts the specified XML subtree into a formatted string for "pretty printing". If no arguments are passed, the entire XML tree is converted.
### Arguments

### Return value

Multi-line indented output of the specified XML subtree.
## int setIntArg ( string name , int value , int radix = 10 )

Sets a value for a given *int* argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *string* **name** - Name of an argument.
- *int* **value** - Value of an argument.
- *int* **radix** - Radix to use when setting a value.

### Return value

**1** if the value is set successfully; otherwise, **0**.
## int getIntArg ( string name )


Returns a value of a given *int* argument.


> **Notice:** To check whether the argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int getIntArg ( string name , int value )


Returns a value of a given *int* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *int* **value** - Default value of the argument.

### Return value

Argument value.
## bool setIntArrayData ( int[] src , int radix )

Sets a vector of integers as a content for the XML node in a given number notation. By default, the decimal number notation is used. This can be done only for XML nodes with no children.
### Arguments

- *int[]* **src** - Reference to a [*vector*](../../../code/uniginescript/language/containers/index.md#vector).
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the content is set successfully; otherwise, false.
## int setIntData ( int value , int radix = 10 )

Sets an integer as a content for the XML node in a given number notation. By default, the decimal number notation is used. This can be done only for XML nodes with no children.
### Arguments

- *int* **value** - Content to set.
- *int* **radix** - Radix to use when setting a value.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## int getIntData ( )

Returns an integer interpretation of data stored in the node.
### Return value

Data stored in the node.
## int setIVec2Arg ( string name , ivec2 value )

Sets a value of a given *ivec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec2* **value** - Value of an argument.

### Return value

Always **1**.
## ivec2 getIVec2Arg ( string name )


Returns a value of a given *ivec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setIVec3Arg ( string name , ivec3 value )

Sets a value of a given *ivec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec3* **value** - Value of an argument.

### Return value

Always **1**.
## ivec3 getIVec3Arg ( string name )


Returns a value of a given *ivec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setIVec4Arg ( string name , ivec4 value )

Sets a value of a given *ivec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec4* **value** - Value of an argument.

### Return value

Always **1**.
## ivec4 getIVec4Arg ( string name )


Returns a value of a given *ivec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setMat4Arg ( string name , mat4 value )

Sets a value of a given *mat4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *mat4* **value** - Value of an argument.

### Return value

Always **1**.
## mat4 getMat4Arg ( string name )


Returns a value of a given *mat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setQuatArg ( string name , quat value )

Sets a value of a given *quat* argument.
### Arguments

- *string* **name** - Name of an argument.
- *quat* **value** - Value of an argument.

### Return value

Always **1**.
## quat getQuatArg ( string name )


Returns a value of a given *quat* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setRawData ( string data )

Sets a raw content for the node. Raw data will be automatically formatted as a CDATA section. This can be done only for nodes with no children.
### Arguments

- *string* **data** - Content to set.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## bool setStringArrayArg ( )

Sets a vector of strings as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

### Return value

Always **1**.
## bool getStringArrayArg ( )

Returns a set of string values stored in an argument and puts them in a vector.
### Arguments

### Return value

**1** if *dest* contains anything; otherwise, **0**.
## String getSubTree ( string path = 0 )

Dumps the node tree.
### Arguments

- *string* **path** - Path to the node. See the description of [*find()*](#find_cstr_Xml) for more details.

### Return value

Single-line non-indented output of the node tree. If no arguments are passed, the entire XML tree would be output.
## int setVec2Arg ( string name , vec2 value )

Sets a value of a given *vec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec2* **value** - Value of an argument.

### Return value

Always **1**.
## vec2 getVec2Arg ( string name )


Returns a value of a given *vec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setVec3Arg ( string name , vec3 value )

Sets a value of a given *vec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec3* **value** - Value of an argument.

### Return value

Always **1**.
## vec3 getVec3Arg ( string name )


Returns a value of a given *vec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setVec4Arg ( string name , vec4 value )

Sets a value of a given *vec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec4* **value** - Value of an argument.

### Return value

Always **1**.
## vec4 getVec4Arg ( string name )


Returns a value of a given *vec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int setXmlData ( string data )

Sets an unquoted string to data stored in the node. This string can also contain XML sub-tree with rich text formatting.
### Arguments

- *string* **data** - Unquoted string to set.

### Return value

**1** if the string is set successfully; otherwise, **0**.
## addChild ( )

Appends a new XML node to the current XML node as a child.
### Arguments

### Return value

Created XML node.
## addChild ( )

Appends a new XML node to the current XML node as a child.
### Arguments

### Return value

Created XML node.
## void clear ( )

Clears all data associated with the node.
## void clearChildren ( )

Clears all children of the current XML node.
## void clearUnusedData ( )

Clears the unused nodes and arguments.
## void copy ( Xml source )

Copies all data (name, arguments, data, flags and a child hierarchy) from the source XML node to the current one.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **source** - Source XML node.

## String decode ( string arg1 )

Decodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) and numeric character references.
### Arguments

- *string* **arg1** - Data to decode.

### Return value

Decoded string.
## String encode ( string arg1 )

Encodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) to their character entity reference.
### Arguments

- *string* **arg1** - Data to encode.

### Return value

Encoded string.
## int findArg ( string name )

Searches for a XML argument by its name.
### Arguments

- *string* **name** - XML argument name.

### Return value

XML argument number.
## int findChild ( string name )

Searches for the number of the XML node child by name.
### Arguments

- *string* **name** - Name of the XML node child.

### Return value

The number of the XML node child if it is exists; otherwise, -1.
## bool load ( bool skip_errors = false )

Loads an XML document and sets the current node to be the root of the parsed tree.
### Arguments

- *bool* **skip_errors** - **1** to enable automatic skipping of errors (the file will be loaded in any case); **0** � to disable it (the file will not be loaded in case of any error).

### Return value

**1** if the file is read and parsed successfully; otherwise, **0**.
## int parse ( string src )

Parses a string with XML mark-up and sets the current node to be the root of the parsed tree.
### Arguments

- *string* **src** - String with an XML content.

### Return value

**1** if a string is successfully parsed; otherwise **0**.
## void printUnusedData ( string name )

Logs warnings of unused data for debugging.
### Arguments

- *string* **name** - Path to the file.

## int removeArg ( string name )

Removes the argument with the given name from the list of the current XML node arguments.
### Arguments

- *string* **name** - Name of the target argument.

### Return value

1 if the argument is deleted successfully; otherwise, 0.
## removeChild ( )

Removes a child node and its descendants from the current XML node.
### Arguments

### Return value

Removed child node and its descendants, if they are found; otherwise, 0.
## bool save ( bool binary = false )

Formats the tree of the current node and writes it to the specified file in the specified format. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *bool* **binary** - Binary format flag: use true to save data to a binary file, or false - to save it to a text file.

### Return value

true if the file is written successfully; otherwise, false.
## String symbols ( string arg1 )

Replaces ampersand characters with character entity references.
### Arguments

- *string* **arg1** - String to encode.

### Return value

String which contains replaced ampersand characters with character entity references.
## int setPaletteArg ( string name , Palette value )

Sets a *palette* value of a given argument.
### Arguments

- *string* **name** - The argument name.
- *[Palette](../../../api/library/common/class.palette_usc.md)* **value** - The argument value.

### Return value

Always **1**.
## Palette getPaletteArg ( string name )

Returns a *palette* value of a specified argument.
### Arguments

- *string* **name** - The argument name.

### Return value

Value of the argument, if it is found; otherwise, **0**.
## void setPaletteData ( Palette data )

Sets a *palette* content for the node. This can be done only for nodes with no children.
### Arguments

- *[Palette](../../../api/library/common/class.palette_usc.md)* **data** - Content to set.

## Palette getPaletteData ( )

Returns a *palette* interpretation of data stored in the node.
### Return value

Data stored in the node.
## int setLongArg ( string name , long value , int radix = 10 )

Sets a *long* value of a given argument.
### Arguments

- *string* **name** - The argument name.
- *long* **value** - The argument value.
- *int* **radix** - Radix (base) specifying the form of representation of the value, one of the following:

  - 2 - binary
  - 8 - octal
  - 10 - decimal (default)
  - 16 - hexadecimal

### Return value

Always **1**.
## long getLongArg ( string name )


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - The argument name.

### Return value

The argument value.
## long getLongArg ( string name , long value )


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - The argument name.
- *long* **value** - Default value of the argument.

### Return value

The argument value.
## bool setIntArrayArg ( int[] src , int radix = 10 )

Sets the specified array of *int* elements as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *int[]* **src** - Reference to a [*vector*](../../../code/uniginescript/language/containers/index.md#vector).
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the array is set successfully; otherwise, false.
