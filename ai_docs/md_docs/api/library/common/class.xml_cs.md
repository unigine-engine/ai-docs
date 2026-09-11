# Unigine::Xml Class (CS)


As Unigine extensively uses XML for storing different types of data, it also provides functionality for parsing and saving files of this type.


### Example


The example below creates an Xml and prints all added data to the console.


```csharp
private static Xml my_xml_create()
{
	// creating the xml with a root element
	Xml xml = new Xml("xml_element");

	// adding children
	Xml xml_0 = xml.AddChild("child", "arg=\"0\"");
	Xml xml_1 = xml_0.AddChild("child1", "arg=\"1\"");
	Xml xml_2 = xml_1.AddChild("child2", "arg=\"2\"");

	// setting data to a child element
	xml_2.Data = "data";

	return xml;
}

// method to print the Xml data to the console
private static void my_xml_print(Xml xml, int offset = 0)
{
	// creating indents
	for (int i = 0; i < offset; i++)
	{
		Log.Message(" ");
	}

	//printing xml info
	Log.Message("{0}: ", xml.Name);
	for (int i = 0; i < xml.NumArgs; i++)
	{
		Log.Message("{0}={1} ", xml.GetArgName(i), xml.GetArgValue(i));
	}

	Log.Message(": {0}\n", xml.Data);
	for (int i = 0; i < xml.NumChildren; i++)
	{
		my_xml_print(xml.GetChild(i), offset + 1);
	}
}

private void Init()
{

	// create xml tree
	Xml xml = my_xml_create();

	// print xml tree
	my_xml_print(xml);

}

```


### See Also


- C++ sample
- C# sample


## Xml Class

### Properties

## quat QuatData

The quaternion interpretation of data stored in the node.
## dmat4 DMat4Data

The *dmat4* matrix interpretation of data stored in the node.
## mat4 Mat4Data

The *mat4* matrix interpretation of data stored in the node.
## ivec4 IVec4Data

The *ivec4* interpretation of data stored in the node.
## ivec3 IVec3Data

The *ivec3* interpretation of data stored in the node.
## ivec2 IVec2Data

The *ivec2* interpretation of data stored in the node.
## dvec4 DVec4Data

The *dvec4* interpretation of data stored in the node.
## dvec3 DVec3Data

The *dvec3* interpretation of data stored in the node.
## dvec2 DVec2Data

The *dvec2* interpretation of data stored in the node.
## vec4 Vec4Data

The *vec4* interpretation of data stored in the node.
## vec3 Vec3Data

The *vec3* interpretation of data stored in the node.
## vec2 Vec2Data

The *vec2* interpretation of data stored in the node.
## double DoubleData

The *double* interpretation of data stored in the node.
## float FloatData

The *float* interpretation of data stored in the node.
## long LongData

The *long* interpretation of data stored in the node.
## bool BoolData

The boolean interpretation of data stored in the node.
## string Data

The data from the XML file.
## 🔒︎ int NumArgs

The number of arguments.
## 🔒︎ int NumChildren

The number of the node children.
## string Name

The name of the node.
## 🔒︎ string LoadPath

The path to an XML file from which the data of the XML instance was loaded.
## Palette PaletteData

The palette interpretation of data.
### Members

---

## Xml ( )

Default constructor that creates an empty instance.
## Xml ( string name , string args = 0 )

Creates an XML tree with a given node as a root.
### Arguments

- *string* **name** - Name of the node that will be a root.
- *string* **args** - Optional arguments to the root node. If provided, they should be in this form: *arg1=\"value1\" arg2=\"value2\" �* If values do not contain spaces, escaped quotes can be omitted.

## Xml ( Xml xml )

Constructor. Creates a path out of the specified XML file.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - XML file instance.

## bool SetArg ( string name , string value )

Sets a literal value of a given argument.
### Arguments

- *string* **name** - The XML argument name.
- *string* **value** - The XML argument value.

### Return value

true if the argument is set successfully; otherwise, false.
## string GetArg ( string name )

Returns an XML argument.
### Arguments

- *string* **name** - The XML argument name.

### Return value

Value of the argument, if it is found; otherwise, **0**.
## bool IsArg ( string name )

Checks whether an argument with a given name exists.
### Arguments

- *string* **name** - Name to check.

### Return value

true if the argument exists; otherwise, false.
## void SetArgName ( int num , string name )

Sets the XML argument name.
### Arguments

- *int* **num** - The argument number.
- *string* **name** - The argument name.

## string GetArgName ( int num )

Returns argument name by its number.
### Arguments

- *int* **num** - Argument number.

### Return value

Argument name.
## void SetArgValue ( int num , string value )

Sets the XML argument value.
### Arguments

- *int* **num** - The argument number.
- *string* **value** - The argument value.

## string GetArgValue ( int num )

Returns the XML argument value.
### Arguments

- *int* **num** - The argument number.

### Return value

Argument value.
## bool SetBoolArg ( string name , bool value )

Sets a value of a given boolean argument.
### Arguments

- *string* **name** - Name of an argument.
- *bool* **value** - Value of the argument. Any non-zero value means true, the zero value means false.

### Return value

true if the operation was successful; otherwise, false.
## bool GetBoolArg ( string name , bool value )


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *bool* **value** - Default value of the argument.

### Return value

**1** if the argument has a value 1, true or TRUE; **0**, if the argument has a value 0, false or FALSE; otherwise, **0**.
## bool GetBoolArg ( string name )


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

true if the argument has a value of 1, true or TRUE; or false, if the argument has a value 0, false or FALSE; otherwise, 0.
## Xml GetChild ( string name )

Returns the child of the XML tree.
### Arguments

- *string* **name** - The child number.

### Return value

XML instance.
## Xml GetChild ( int num )


Returns a child node by its name or index number in the child list.


> **Notice:** To check if a child with a given name exists, use the [*isChild()*](#isChild_cstr_int) method.


### Arguments

- *int* **num** - The child number.

### Return value

Target child node, if it is found; otherwise, **0**.
## bool IsChild ( string name )

Checks if a child element with a given name exists.
### Arguments

- *string* **name** - Element name to check.

### Return value

true if a child with the provided name exists; otherwise, false.
## string GetChildData ( string name )

Returns the data from the XML child node.
### Arguments

- *string* **name** - Name of the child node.

### Return value

The value of the child node.
## bool SetDMat4Arg ( string name , dmat4 value )

Sets a value of a given *dmat4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dmat4* **value** - Value of an argument.

### Return value

Always true.
## dmat4 GetDMat4Arg ( string name )


Returns a value of a given *dmat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetDoubleArg ( string name , double value )

Sets a value of a given *double* argument.
### Arguments

- *string* **name** - Name of an argument.
- *double* **value** - Value of an argument.

### Return value

Always **1**.
## double GetDoubleArg ( string name , double value )


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *double* **value** - Default value of the argument.

### Return value

Argument value.
## double GetDoubleArg ( string name )


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetDoubleArrayArg ( string name , double[] OUT_src , int src_size )

Sets the specified array of *double* elements as a value of a given argument.
### Arguments

- *string* **name** - Name of an argument.
- *double[]* **OUT_src** - Source array with *double* elements. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

Always true.
## bool GetDoubleArrayArg ( string name , ref double[] dest , int dest_size )

Retrieves a set of *double* values stored in an argument and puts them to the specified array.
### Arguments

- *string* **name** - Name of an argument.
- *ref double[]* **dest** - Target array with *double* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool SetDoubleArrayData ( double[] OUT_src , int src_size )

Sets the specified array of *double* values as the content for the node. This can be done only for nodes with no children.
### Arguments

- *double[]* **OUT_src** - Source array that contains the data to be set for the node. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

true if the content is set successfully; otherwise, false.
## bool GetDoubleArrayData ( ref double[] dest , int dest_size )

Retrieves an interpretation of data stored in the node and puts it to the specified array as *double* values.
### Arguments

- *ref double[]* **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## bool SetDVec2Arg ( string name , dvec2 value )

Sets a value of a given *dvec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec2* **value** - Value of an argument.

### Return value

Always **1**.
## dvec2 GetDVec2Arg ( string name )

Returns a value of a given *dvec2* argument.
> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetDVec3Arg ( string name , dvec3 value )

Sets a value of a given *dvec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec3* **value** - Value of an argument.

### Return value

Always **1**.
## dvec3 GetDVec3Arg ( string name )


Returns a value of a given *dvec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetDVec4Arg ( string name , dvec4 value )

Sets a value of a given *dvec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *dvec4* **value** - Value of an argument.

### Return value

Always **1**.
## dvec4 GetDVec4Arg ( string name )


Returns a value of a given *dvec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetFloatArg ( string name , float value )

Sets a value of a given *float* argument.
### Arguments

- *string* **name** - Name of an argument.
- *float* **value** - Value of an argument.

### Return value

Always **1**.
## float GetFloatArg ( string name , float value )


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *float* **value** - Default value of the argument.

### Return value

Argument value.
## float GetFloatArg ( string name )


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetFloatArrayArg ( string name , float[] OUT_src , int src_size )

Sets the specified array of *float* elements as a value of a given argument.
### Arguments

- *string* **name** - Name of an argument.
- *float[]* **OUT_src** - Source array with *float* elements. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

Always true.
## bool GetFloatArrayArg ( string name , ref float[] dest , int dest_size )

Retrieves a set of *float* values stored in an argument and puts them to the specified array.
### Arguments

- *string* **name** - Name of an argument.
- *ref float[]* **dest** - Target array with *float* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool SetFloatArrayData ( float[] OUT_src , int src_size )

Sets the specified array of *float* values as the content for the node. This can be done only for nodes with no children.
### Arguments

- *float[]* **OUT_src** - Source array that contains the data to be set for the node. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

true if the content is set successfully; otherwise, false.
## bool GetFloatArrayData ( ref float[] dest , int dest_size )

Retrieves an interpretation of data stored in the node and puts it to the specified array as *float* values.
### Arguments

- *ref float[]* **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## string GetFormattedSubTree ( string path = 0 , string indent = "\t" )

Converts the specified XML subtree into a formatted string for "pretty printing". If no arguments are passed, the entire XML tree is converted.
### Arguments

- *string* **path** - Path to the XML subtree to be formatted. See the description of [*find()*](#find_cstr_Xml) for more details.
- *string* **indent** - String to be used for indenting (e.g. "\t").

### Return value

Multi-line indented output of the specified XML subtree.
## bool SetIntArg ( string name , int value , int radix = 10 )

Sets a value for a given *int* argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *string* **name** - Name of an argument.
- *int* **value** - Value of an argument.
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the value is set successfully; otherwise, false.
## int GetIntArg ( string name )


Returns a value of a given *int* argument.


> **Notice:** To check whether the argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## int GetIntArg ( string name , int value )


Returns a value of a given *int* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.
- *int* **value** - Default value of the argument.

### Return value

Argument value.
## bool SetIntArrayData ( int[] src , int radix )

Sets a vector of integers as a content for the XML node in a given number notation. By default, the decimal number notation is used. This can be done only for XML nodes with no children.
### Arguments

- *int[]* **src** - Reference to a [*vector*](../../../code/uniginescript/language/containers/index.md#vector).
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the content is set successfully; otherwise, false.
## bool GetIntArrayData ( ref int[] dest , int dest_size )

Retrieves an interpretation of data stored in the node and puts it to the specified array as *int* values.
### Arguments

- *ref int[]* **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## bool SetIntData ( int value , int radix = 10 )

Sets an integer as a content for the XML node in a given number notation. By default, the decimal number notation is used. This can be done only for XML nodes with no children.
### Arguments

- *int* **value** - Content to set.
- *int* **radix** - Radix to use when setting a value.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## int GetIntData ( )

Returns an integer interpretation of data stored in the node.
### Return value

Data stored in the node.
## bool SetIVec2Arg ( string name , ivec2 value )

Sets a value of a given *ivec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec2* **value** - Value of an argument.

### Return value

Always **1**.
## ivec2 GetIVec2Arg ( string name )


Returns a value of a given *ivec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetIVec3Arg ( string name , ivec3 value )

Sets a value of a given *ivec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec3* **value** - Value of an argument.

### Return value

Always **1**.
## ivec3 GetIVec3Arg ( string name )


Returns a value of a given *ivec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetIVec4Arg ( string name , ivec4 value )

Sets a value of a given *ivec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *ivec4* **value** - Value of an argument.

### Return value

Always **1**.
## ivec4 GetIVec4Arg ( string name )


Returns a value of a given *ivec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetMat4Arg ( string name , mat4 value )

Sets a value of a given *mat4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *mat4* **value** - Value of an argument.

### Return value

Always **1**.
## mat4 GetMat4Arg ( string name )


Returns a value of a given *mat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## Xml GetParent ( )

Returns the parent of the current XML node.
### Return value

XML node.
## bool SetQuatArg ( string name , quat value )

Sets a value of a given *quat* argument.
### Arguments

- *string* **name** - Name of an argument.
- *quat* **value** - Value of an argument.

### Return value

Always **1**.
## quat GetQuatArg ( string name )


Returns a value of a given *quat* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetRawData ( string data )

Sets a raw content for the node. Raw data will be automatically formatted as a CDATA section. This can be done only for nodes with no children.
### Arguments

- *string* **data** - Content to set.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## bool SetStringArrayArg ( string name , string[] src )

Sets a vector of strings as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *string* **name** - Name of an argument.
- *string[]* **src** - An array of strings.

### Return value

Always **1**.
## bool GetStringArrayArg ( string name , string[] OUT_dest )

Returns a set of string values stored in an argument and puts them in a vector.
### Arguments

- *string* **name** - Name of the string.
- *string[]* **OUT_dest** - Reference to a [*vector*](../../../code/uniginescript/language/containers/index.md#vector). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

**1** if *dest* contains anything; otherwise, **0**.
## bool SetStringArrayData ( string[] src , string delimiter = "," )

Sets a vector of strings as a content for the node. This can be done only for nodes with no children.
### Arguments

- *string[]* **src** - [*Vector*](../../../api/library/containers/vector/class.vector_cs.md) of strings.
- *string* **delimiter** - Character(s) to be used as a delimiter to split tokens.

### Return value

true if the content is set successfully; otherwise, false.
## bool GetStringArrayData ( string[] OUT_dest , string delimiter = "," )

Returns an interpretation of data stored in the node as a vector of strings.
### Arguments

- *string[]* **OUT_dest** - [*Vector*](../../../api/library/containers/vector/class.vector_cs.md) of strings. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *string* **delimiter** - Character(s) to be used as a delimiter to split tokens.

### Return value

**1** if *dest* contains anything; otherwise, **0**.
## string GetSubTree ( string path = 0 )

Dumps the node tree.
### Arguments

- *string* **path** - Path to the node. See the description of [*find()*](#find_cstr_Xml) for more details.

### Return value

Single-line non-indented output of the node tree. If no arguments are passed, the entire XML tree would be output.
## bool SetVec2Arg ( string name , vec2 value )

Sets a value of a given *vec2* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec2* **value** - Value of an argument.

### Return value

Always **1**.
## vec2 GetVec2Arg ( string name )


Returns a value of a given *vec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetVec3Arg ( string name , vec3 value )

Sets a value of a given *vec3* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec3* **value** - Value of an argument.

### Return value

Always **1**.
## vec3 GetVec3Arg ( string name )


Returns a value of a given *vec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetVec4Arg ( string name , vec4 value )

Sets a value of a given *vec4* argument.
### Arguments

- *string* **name** - Name of an argument.
- *vec4* **value** - Value of an argument.

### Return value

Always **1**.
## vec4 GetVec4Arg ( string name )


Returns a value of a given *vec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - Name of a target argument.

### Return value

Argument value.
## bool SetXmlData ( string data )

Sets an unquoted string to data stored in the node. This string can also contain XML sub-tree with rich text formatting.
### Arguments

- *string* **data** - Unquoted string to set.

### Return value

true if the string is set successfully; otherwise, false.
## Xml AddChild ( string name , string args = 0 )

Appends a new XML node to the current XML node as a child.
### Arguments

- *string* **name** - Name of the XML node.
- *string* **args** - Arguments of the XML node. The default value is 0. > **Notice:** This value should be passed if the first argument is a string

### Return value

Created XML node.
## Xml AddChild ( Xml xml )

Appends a new XML node to the current XML node as a child.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Argument of one of the following types:

  - *Xml* **xml** - XML node.
  - *string* **name** - Name of the XML node.

### Return value

Created XML node.
## void Clear ( )

Clears all data associated with the node.
## void ClearChildren ( )

Clears all children of the current XML node.
## void ClearUnusedData ( )

Clears the unused nodes and arguments.
## void Copy ( Xml source )

Copies all data (name, arguments, data, flags and a child hierarchy) from the source XML node to the current one.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **source** - Source XML node.

## string Decode ( string arg1 )

Decodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) and numeric character references.
### Arguments

- *string* **arg1** - Data to decode.

### Return value

Decoded string.
## string Encode ( string arg1 )

Encodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) to their character entity reference.
### Arguments

- *string* **arg1** - Data to encode.

### Return value

Encoded string.
## Xml Find ( string path )

Searches for an XML sub-tree.
### Arguments

- *string* **path** - Path to the XML sub-tree.

### Return value

XML node.
## int FindArg ( string name )

Searches for a XML argument by its name.
### Arguments

- *string* **name** - XML argument name.

### Return value

XML argument number.
## int FindChild ( string name )

Searches for the number of the XML node child by name.
### Arguments

- *string* **name** - Name of the XML node child.

### Return value

The number of the XML node child if it is exists; otherwise, -1.
## bool Load ( string name , bool skip_errors = false )

Loads an XML document and sets the current node to be the root of the parsed tree.
### Arguments

- *string* **name** - File name.
- *bool* **skip_errors** - true to enable automatic skipping of errors (the file will be loaded in any case); false � to disable it (the file will not be loaded in case of any error).

### Return value

true if the file is read and parsed successfully; otherwise, false.
## bool Load ( Stream stream , ulong read_size , bool binary = false , bool skip_errors = false )

Loads XML data from the specified stream and sets the current node to be the root of the parsed tree.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream from which the data of the XML node is to be loaded.
- *ulong* **read_size** - Size of the data block to be read from the stream, in bytes.
- *bool* **binary** - Binary format flag: use true to load data in binary format, or false - to load it in text format.
- *bool* **skip_errors** - true to enable automatic skipping of errors (the data will be loaded in any case); false � to disable it (the data will not be loaded in case of any error).

### Return value

true if the data is read and parsed successfully; otherwise, false.
## bool Parse ( string src )

Parses a string with XML mark-up and sets the current node to be the root of the parsed tree.
### Arguments

- *string* **src** - String with an XML content.

### Return value

true if a string is successfully parsed; otherwise false.
## void PrintUnusedData ( string name )

Logs warnings of unused data for debugging.
### Arguments

- *string* **name** - Path to the file.

## int RemoveArg ( string name )

Removes the argument with the given name from the list of the current XML node arguments.
### Arguments

- *string* **name** - Name of the target argument.

### Return value

1 if the argument is deleted successfully; otherwise, 0.
## Xml RemoveChild ( Xml xml )

Removes a child node and its descendants from the current XML node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - XML sub-tree smart pointer.

### Return value

Removed child node and its descendants, if they are found; otherwise, 0.
## bool Save ( string name , bool binary = false , string indent = "\t" )

Formats the tree of the current node and writes it to the specified file in the specified format. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *string* **name** - Path to the file.
- *bool* **binary** - Binary format flag: use true to save data to a binary file, or false - to save it to a text file.
- *string* **indent** - String to be used for indentation (e.g. "\t").

### Return value

true if the file is written successfully; otherwise, false.
## bool Save ( Stream stream , bool binary = false , string indent = "\t" )

Formats the tree of the current node and writes is to the specified stream in the specified format.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data of the XML node is to be written.
- *bool* **binary** - Binary format flag: use true to save data to a binary file, or false - to save it to a text file.
- *string* **indent** - String to be used for indentation (e.g. "\t").

### Return value

true if the file is written successfully; otherwise, false.
## string Symbols ( string arg1 )

Replaces ampersand characters with character entity references.
### Arguments

- *string* **arg1** - String to encode.

### Return value

String which contains replaced ampersand characters with character entity references.
## bool SetData ( UGUID guid )

Sets a UGUID content for the node.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( bool value )

Sets a boolean content for the node.
### Arguments

- *bool* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( int value , int radix = 10 )

Sets an integer content in the specified form (binary, octal, decimal, hexadecimal) for the node.
### Arguments

- *int* **value** - Content to set.
- *int* **radix** - Radix (base) specifying the form of representation of the value, one of the following:

  - 2 - binary
  - 8 - octal
  - 10 - decimal (default)
  - 16 - hexadecimal

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( long value )

Sets a long integer content for the node.
### Arguments

- *long* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( float value )

Sets a float content for the node.
### Arguments

- *float* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( double value )

Sets a double content for the node.
### Arguments

- *double* **value**

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( vec2 value )

Sets a vec2 vector content for the node.
### Arguments

- *vec2* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( vec3 value )

Sets a vec3 vector content for the node.
### Arguments

- *vec3* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( vec4 value )

Sets a vec4 vector content for the node.
### Arguments

- *vec4* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( dvec2 value )

Sets a dvec2 vector content for the node.
### Arguments

- *dvec2* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( dvec3 value )

Sets a dvec3 vector content for the node.
### Arguments

- *dvec3* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( dvec4 value )

Sets a dvec4 vector content for the node.
### Arguments

- *dvec4* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( ivec3 value )

Sets an ivec3 vector content for the node.
### Arguments

- *ivec3* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( ivec2 value )

Sets an ivec2 vector content for the node.
### Arguments

- *ivec2* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( ivec4 value )

Sets an ivec4 vector content for the node.
### Arguments

- *ivec4* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( mat4 value )

Sets a mat4 matrix content for the node.
### Arguments

- *mat4* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( dmat4 value )

Sets a dmat4 matrix content for the node.
### Arguments

- *dmat4* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( quat value )

Sets a quaternion content for the node.
### Arguments

- *quat* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool SetData ( Palette value )

Sets a palette content for the node.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## void ReadChildData ( string name , out bool value )

Reads a boolean interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out bool* **value** - Target boolean variable.

## void ReadChildData ( string name , out int value )

Reads an integer interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out int* **value** - Target integer variable.

## void ReadChildData ( string name , out byte value )

Reads a character interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out byte* **value** - Target character variable.

## void ReadChildData ( string name , out long value )

Reads a long integer interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out long* **value** - Target long integer variable.

## void ReadChildData ( string name , out float value )

Reads a float interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out float* **value** - Target float variable.

## void ReadChildData ( string name , out double value )

Reads a double interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out double* **value** - Target double variable.

## void ReadChildData ( string name , out vec2 value )

Reads a vec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out vec2* **value** - Target vec2 variable.

## void ReadChildData ( string name , out vec3 value )

Reads a vec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out vec3* **value** - Target vec3 variable.

## void ReadChildData ( string name , out vec4 value )

Reads a vec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out vec4* **value** - Target vec4 variable.

## void ReadChildData ( string name , out dvec2 value )

Reads a dvec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out dvec2* **value** - Target dvec2 variable.

## void ReadChildData ( string name , out dvec3 value )

Reads a dvec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out dvec3* **value** - Target dvec3 variable.

## void ReadChildData ( string name , out dvec4 value )

Reads a dvec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out dvec4* **value** - Target dvec4 variable.

## void ReadChildData ( string name , out ivec2 value )

Reads an ivec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out ivec2* **value** - Target ivec2 variable.

## void ReadChildData ( string name , out ivec3 value )

Reads an ivec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out ivec3* **value** - Target ivec3 variable.

## void ReadChildData ( string name , out ivec4 value )

Reads an ivec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out ivec4* **value** - Target ivec4 variable.

## void ReadChildData ( string name , out mat4 value )

Reads a mat4 matrix interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out mat4* **value** - Target mat4 variable.

## void ReadChildData ( string name , out dmat4 value )

Reads a dmat4 matrix interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out dmat4* **value** - Target dmat4 variable.

## void ReadChildData ( string name , out Palette value )

Reads a palette interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Child node name.
- *out [Palette](../../../api/library/common/class.palette_cs.md)* **value** - Target palette variable.

## void ReadArg ( string name , out bool value )

Reads a boolean interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out bool* **value** - Target boolean variable.

## void ReadArg ( string name , out int value )

Reads an integer interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out int* **value** - Target integer variable.

## void ReadArg ( string name , out byte value )

Reads a character interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out byte* **value** - Target character variable.

## void ReadArg ( string name , out float value )

Reads a float interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out float* **value** - Target float variable.

## void ReadArg ( string name , out double value )

Reads a double interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out double* **value** - Target double variable.

## void ReadArg ( string name , out vec2 value )

Reads a vec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out vec2* **value** - Target vec2 variable.

## void ReadArg ( string name , out vec3 value )

Reads a vec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out vec3* **value** - Target vec3 variable.

## void ReadArg ( string name , out vec4 value )

Reads a vec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out vec4* **value** - Target vec4 variable.

## void ReadArg ( string name , out dvec2 value )

Reads a dvec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out dvec2* **value** - Target dvec2 variable.

## void ReadArg ( string name , out dvec3 value )

Reads a dvec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out dvec3* **value** - Target dvec3 variable

## void ReadArg ( string name , out dvec4 value )

Reads a dvec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out dvec4* **value** - Target dvec4 variable.

## void ReadArg ( string name , out ivec2 value )

Reads a ivec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out ivec2* **value** - Target ivec2 variable.

## void ReadArg ( string name , out ivec3 value )

Reads a ivec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out ivec3* **value** - Target ivec3 variable.

## void ReadArg ( string name , out ivec4 value )

Reads a ivec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out ivec4* **value** - Target ivec4 variable.

## void ReadArg ( string name , out Palette value )

Reads a *palette* interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *string* **name** - Name of the target argument.
- *out [Palette](../../../api/library/common/class.palette_cs.md)* **value** - Target palette variable.

## bool SetPaletteArg ( string name , Palette value )

Sets a *palette* value of a given argument.
### Arguments

- *string* **name** - The argument name.
- *[Palette](../../../api/library/common/class.palette_cs.md)* **value** - The argument value.

### Return value

Always **1**.
## Palette GetPaletteArg ( string name )

Returns a *palette* value of a specified argument.
### Arguments

- *string* **name** - The argument name.

### Return value

Value of the argument, if it is found; otherwise, **0**.
## bool SetLongArg ( string name , long value , int radix = 10 )

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
## long GetLongArg ( string name )


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - The argument name.

### Return value

The argument value.
## long GetLongArg ( string name , long value )


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *string* **name** - The argument name.
- *long* **value** - Default value of the argument.

### Return value

The argument value.
## bool SetLongArrayArg ( string name , llong[] src , int radix = 10 )

Sets the specified array of *long* elements as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *string* **name** - The argument name.
- *llong[]* **src** - An array of long values.
- *int* **radix** - Radix (base) specifying the form of representation of the value, one of the following:

  - 2 - binary
  - 8 - octal
  - 10 - decimal (default)
  - 16 - hexadecimal

### Return value

true if the array is set successfully; otherwise, false.
## bool GetLongArrayArg ( string name , ref llong[] dest , int dest_size )

Retrieves a set of *long* values stored in an argument and puts them to the specified array.
### Arguments

- *string* **name** - Name of a target argument.
- *ref llong[]* **dest** - Target array with *llong* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool SetIntArrayArg ( string name , int[] src , int radix = 10 )

Sets the specified array of *int* elements as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *string* **name** - Name of an argument.
- *int[]* **src** - An array of integers.
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the array is set successfully; otherwise, false.
## bool GetIntArrayArg ( string name , ref int[] dest , int dest_size )

Retrieves a set of *int* values stored in an argument and puts them to the specified array.
### Arguments

- *string* **name** - Name of a target argument.
- *ref int[]* **dest** - Target array with *int* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
