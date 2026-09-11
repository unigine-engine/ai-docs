# Unigine::Xml Class (CPP)

**Header:** #include <UnigineXml.h>


As Unigine extensively uses XML for storing different types of data, it also provides functionality for parsing and saving files of this type.


### Example


The example below creates an Xml and prints all added data to the console.


```cpp
#include "AppWorldLogic.h"

using namespace Unigine;

XmlPtr my_xml_create()
{
	// creating the xml with a root element
	XmlPtr xml = Xml::create("xml_element");

	// adding children
	XmlPtr xml_0 = xml->addChild("child", "arg=\"0\"");
	XmlPtr xml_1 = xml_0->addChild("child1", "arg=\"1\"");
	XmlPtr xml_2 = xml_1->addChild("child2", "arg=\"2\"");

	// setting data to a child element
	xml_2->setData("data");

	return xml;
}

// method to print the Xml data to the console
void my_xml_print(XmlPtr xml, int offset=0)
{
	// creating indents
	for (int i = 0; i < offset; i++)
		Log::message(" ");

	//printing xml info
	Log::message("%s: ", xml->getName());

	for (int i = 0; i < xml->getNumArgs(); i++)
		Log::message("%s=%s ", xml->getArgName(i), xml->getArgValue(i));

	Log::message(": %s\n", xml->getData());

	for (int i = 0; i < xml->getNumChildren(); i++)
		my_xml_print(XmlPtr(xml->getChild(i)), offset + 1);
}

int AppWorldLogic::init()
{

	// create xml tree
	XmlPtr xml = my_xml_create();

	// print xml tree
	my_xml_print(xml);

	return 1;
}

```


### See Also


- C++ sample
- C# sample


## Xml Class

### Members

## void setQuatData ( const Math:: quat & data )

Sets a new quaternion interpretation of data stored in the node.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md)&* **data** - The quaternion interpretation of data stored in the node.

## Math:: quat getQuatData () const

Returns the current quaternion interpretation of data stored in the node.
### Return value

Current quaternion interpretation of data stored in the node.
## void setDMat4Data ( const Math:: dmat4 & data )

Sets a new *dmat4* matrix interpretation of data stored in the node.
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md)&* **data** - The *dmat4* matrix interpretation of data stored in the node.

## Math:: dmat4 getDMat4Data () const

Returns the current *dmat4* matrix interpretation of data stored in the node.
### Return value

Current *dmat4* matrix interpretation of data stored in the node.
## void setMat4Data ( const Math:: mat4 & data )

Sets a new *mat4* matrix interpretation of data stored in the node.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **data** - The *mat4* matrix interpretation of data stored in the node.

## Math:: mat4 getMat4Data () const

Returns the current *mat4* matrix interpretation of data stored in the node.
### Return value

Current *mat4* matrix interpretation of data stored in the node.
## void setIVec4Data ( const Math:: ivec4 & data )

Sets a new *ivec4* interpretation of data stored in the node.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md)&* **data** - The *ivec4* interpretation of data stored in the node.

## Math:: ivec4 getIVec4Data () const

Returns the current *ivec4* interpretation of data stored in the node.
### Return value

Current *ivec4* interpretation of data stored in the node.
## void setIVec3Data ( const Math:: ivec3 & data )

Sets a new *ivec3* interpretation of data stored in the node.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md)&* **data** - The *ivec3* interpretation of data stored in the node.

## Math:: ivec3 getIVec3Data () const

Returns the current *ivec3* interpretation of data stored in the node.
### Return value

Current *ivec3* interpretation of data stored in the node.
## void setIVec2Data ( const Math:: ivec2 & data )

Sets a new *ivec2* interpretation of data stored in the node.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **data** - The *ivec2* interpretation of data stored in the node.

## Math:: ivec2 getIVec2Data () const

Returns the current *ivec2* interpretation of data stored in the node.
### Return value

Current *ivec2* interpretation of data stored in the node.
## void setDVec4Data ( const Math:: dvec4 & data )

Sets a new *dvec4* interpretation of data stored in the node.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md)&* **data** - The *dvec4* interpretation of data stored in the node.

## Math:: dvec4 getDVec4Data () const

Returns the current *dvec4* interpretation of data stored in the node.
### Return value

Current *dvec4* interpretation of data stored in the node.
## void setDVec3Data ( const Math:: dvec3 & data )

Sets a new *dvec3* interpretation of data stored in the node.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md)&* **data** - The *dvec3* interpretation of data stored in the node.

## Math:: dvec3 getDVec3Data () const

Returns the current *dvec3* interpretation of data stored in the node.
### Return value

Current *dvec3* interpretation of data stored in the node.
## void setDVec2Data ( const Math:: dvec2 & data )

Sets a new *dvec2* interpretation of data stored in the node.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md)&* **data** - The *dvec2* interpretation of data stored in the node.

## Math:: dvec2 getDVec2Data () const

Returns the current *dvec2* interpretation of data stored in the node.
### Return value

Current *dvec2* interpretation of data stored in the node.
## void setVec4Data ( const Math:: vec4 & data )

Sets a new *vec4* interpretation of data stored in the node.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **data** - The *vec4* interpretation of data stored in the node.

## Math:: vec4 getVec4Data () const

Returns the current *vec4* interpretation of data stored in the node.
### Return value

Current *vec4* interpretation of data stored in the node.
## void setVec3Data ( const Math:: vec3 & data )

Sets a new *vec3* interpretation of data stored in the node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **data** - The *vec3* interpretation of data stored in the node.

## Math:: vec3 getVec3Data () const

Returns the current *vec3* interpretation of data stored in the node.
### Return value

Current *vec3* interpretation of data stored in the node.
## void setVec2Data ( const Math:: vec2 & data )

Sets a new *vec2* interpretation of data stored in the node.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **data** - The *vec2* interpretation of data stored in the node.

## Math:: vec2 getVec2Data () const

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
## void setLongData ( long long data )

Sets a new *long* interpretation of data stored in the node.
### Arguments

- *long long* **data** - The *long* interpretation of data stored in the node.

## long long getLongData () const

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
## void setData ( const char * data )

Sets a new data from the XML file.
### Arguments

- *const char ** **data** - The data from the XML file.

## const char * getData () const

Returns the current data from the XML file.
### Return value

Current data from the XML file.
## int getNumArgs () const

Returns the current number of arguments.
### Return value

Current number of arguments.
## int getNumChildren () const

Returns the current number of the node children.
### Return value

Current number of the node children.
## void setName ( const char * name )

Sets a new name of the node.
### Arguments

- *const char ** **name** - The name of the node.

## const char * getName () const

Returns the current name of the node.
### Return value

Current name of the node.
## const char * getLoadPath () const

Returns the current path to an XML file from which the data of the XML instance was loaded.
### Return value

Current path to an XML file from which the data of the XML instance was loaded.
---

## static XmlPtr create ( )

Default constructor that creates an empty instance.
## static XmlPtr create ( const char * name , const char * args = 0 )

Creates an XML tree with a given node as a root.
### Arguments

- *const char ** **name** - Name of the node that will be a root.
- *const char ** **args** - Optional arguments to the root node. If provided, they should be in this form: *arg1=\"value1\" arg2=\"value2\" �* If values do not contain spaces, escaped quotes can be omitted.

## static XmlPtr create ( const Ptr < Xml > & xml )

Constructor. Creates a path out of the specified XML file.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Pointer to the XML file.

## bool setArg ( const char * name , const char * value )

Sets a literal value of a given argument.
### Arguments

- *const char ** **name** - The XML argument name.
- *const char ** **value** - The XML argument value.

### Return value

true if the argument is set successfully; otherwise, false.
## const char * getArg ( const char * name ) const

Returns an XML argument.
### Arguments

- *const char ** **name** - The XML argument name.

### Return value

Value of the argument, if it is found; otherwise, **0**.
## bool isArg ( const char * name ) const

Checks whether an argument with a given name exists.
### Arguments

- *const char ** **name** - Name of XML argument.

### Return value

true if the argument exists; otherwise, false.
## void setArgName ( int num , const char * name )

Sets the XML argument name.
### Arguments

- *int* **num** - The argument number.
- *const char ** **name** - The argument name.

## const char * getArgName ( int num ) const

Returns argument name by its number.
### Arguments

- *int* **num** - Argument number.

### Return value

Argument name.
## void setArgValue ( int num , const char * value )

Sets the XML argument value.
### Arguments

- *int* **num** - The argument number.
- *const char ** **value** - The argument value.

## const char * getArgValue ( int num ) const

Returns the XML argument value.
### Arguments

- *int* **num** - The argument number.

### Return value

Argument value.
## bool setBoolArg ( const char * name , bool value )

Sets a value of a given boolean argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *bool* **value** - Value of the argument. Any non-zero value means true, the zero value means false.

### Return value

true if the operation was successful; otherwise, false.
## bool getBoolArg ( const char * name , bool value ) const


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.
- *bool* **value** - Default value of the argument.

### Return value

**1** if the argument has a value 1, true or TRUE; **0**, if the argument has a value 0, false or FALSE; otherwise, **0**.
## bool getBoolArg ( const char * name ) const


Returns a value of a given boolean argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

true if the argument has a value of 1, true or TRUE; or false, if the argument has a value 0, false or FALSE; otherwise, 0.
## Ptr < Xml > getChild ( const char * name ) const

Returns the child of the XML tree.
### Arguments

- *const char ** **name** - The child number.

### Return value

Pointer to XML.
## Ptr < Xml > getChild ( int num ) const


Returns a child node by its name or index number in the child list.


> **Notice:** To check if a child with a given name exists, use the [*isChild()*](#isChild_cstr_int) method.


### Arguments

- *int* **num** - The child number.

### Return value

Target child node, if it is found; otherwise, **0**.
## bool isChild ( const char * name ) const

Checks if a child element with a given name exists.
### Arguments

- *const char ** **name** - Element name to check.

### Return value

true if a child with the provided name exists; otherwise, false.
## const char * getChildData ( const char * name ) const

Returns the data from the XML child node.
### Arguments

- *const char ** **name** - Name of the child node.

### Return value

The value of the child node.
## bool setDMat4Arg ( const char * name , const Math:: dmat4 & value )

Sets a value of a given *dmat4* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Value of an argument.

### Return value

Always true.
## Math:: dmat4 getDMat4Arg ( const char * name ) const


Returns a value of a given *dmat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setDoubleArg ( const char * name , double value )

Sets a value of a given *double* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *double* **value** - Value of an argument.

### Return value

Always **1**.
## double getDoubleArg ( const char * name , double value ) const


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.
- *double* **value** - Default value of the argument.

### Return value

Argument value.
## double getDoubleArg ( const char * name ) const


Returns a value of a given *double* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setDoubleArrayArg ( const char * name , double* OUT_src , int src_size )

Sets the specified array of *double* elements as a value of a given argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *double** **OUT_src** - Source array with *double* elements. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

Always true.
## bool getDoubleArrayArg ( const char * name , const double* dest , int dest_size ) const

Retrieves a set of *double* values stored in an argument and puts them to the specified array.
### Arguments

- *const char ** **name** - Name of an argument.
- *const double** **dest** - Target array with *double* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool setDoubleArrayData ( double* OUT_src , int src_size )

Sets the specified array of *double* values as the content for the node. This can be done only for nodes with no children.
### Arguments

- *double** **OUT_src** - Source array that contains the data to be set for the node. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

true if the content is set successfully; otherwise, false.
## bool getDoubleArrayData ( const double* dest , int dest_size ) const

Retrieves an interpretation of data stored in the node and puts it to the specified array as *double* values.
### Arguments

- *const double** **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## bool setDVec2Arg ( const char * name , const Math:: dvec2 & value )

Sets a value of a given *dvec2* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: dvec2 getDVec2Arg ( const char * name ) const

Returns a value of a given *dvec2* argument.
> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setDVec3Arg ( const char * name , const Math:: dvec3 & value )

Sets a value of a given *dvec3* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: dvec3 getDVec3Arg ( const char * name ) const


Returns a value of a given *dvec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setDVec4Arg ( const char * name , const Math:: dvec4 & value )

Sets a value of a given *dvec4* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: dvec4 getDVec4Arg ( const char * name ) const


Returns a value of a given *dvec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setFloatArg ( const char * name , float value )

Sets a value of a given *float* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *float* **value** - Value of an argument.

### Return value

Always **1**.
## float getFloatArg ( const char * name , float value ) const


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.
- *float* **value** - Default value of the argument.

### Return value

Argument value.
## float getFloatArg ( const char * name ) const


Returns a value of a given *float* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setFloatArrayArg ( const char * name , float* OUT_src , int src_size )

Sets the specified array of *float* elements as a value of a given argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *float** **OUT_src** - Source array with *float* elements. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

Always true.
## bool getFloatArrayArg ( const char * name , const float* dest , int dest_size ) const

Retrieves a set of *float* values stored in an argument and puts them to the specified array.
### Arguments

- *const char ** **name** - Name of an argument.
- *const float** **dest** - Target array with *float* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool setFloatArrayData ( float* OUT_src , int src_size )

Sets the specified array of *float* values as the content for the node. This can be done only for nodes with no children.
### Arguments

- *float** **OUT_src** - Source array that contains the data to be set for the node. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **src_size** - Array size.

### Return value

true if the content is set successfully; otherwise, false.
## bool getFloatArrayData ( const float* dest , int dest_size ) const

Retrieves an interpretation of data stored in the node and puts it to the specified array as *float* values.
### Arguments

- *const float** **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## String getFormattedSubTree ( const char * path = 0 , const char * indent = "\t" ) const

Converts the specified XML subtree into a formatted string for "pretty printing". If no arguments are passed, the entire XML tree is converted.
### Arguments

- *const char ** **path** - Path to the XML subtree to be formatted. See the description of [*find()*](#find_cstr_Xml) for more details.
- *const char ** **indent** - String to be used for indenting (e.g. "\t").

### Return value

Multi-line indented output of the specified XML subtree.
## bool setIntArg ( const char * name , int value , int radix = 10 )

Sets a value for a given *int* argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *const char ** **name** - Name of an argument.
- *int* **value** - Value of an argument.
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the value is set successfully; otherwise, false.
## int getIntArg ( const char * name ) const


Returns a value of a given *int* argument.


> **Notice:** To check whether the argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## int getIntArg ( const char * name , int value ) const


Returns a value of a given *int* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.
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
## bool getIntArrayData ( const int* dest , int dest_size ) const

Retrieves an interpretation of data stored in the node and puts it to the specified array as *int* values.
### Arguments

- *const int** **dest** - Target array to receive the node's data.
- *int* **dest_size** - Array size.

### Return value

true if values are read successfully; otherwise, false.
## bool setIntData ( int value , int radix = 10 )

Sets an integer as a content for the XML node in a given number notation. By default, the decimal number notation is used. This can be done only for XML nodes with no children.
### Arguments

- *int* **value** - Content to set.
- *int* **radix** - Radix to use when setting a value.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## int getIntData ( ) const

Returns an integer interpretation of data stored in the node.
### Return value

Data stored in the node.
## bool setIVec2Arg ( const char * name , const Math:: ivec2 & value )

Sets a value of a given *ivec2* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: ivec2 getIVec2Arg ( const char * name ) const


Returns a value of a given *ivec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setIVec3Arg ( const char * name , const Math:: ivec3 & value )

Sets a value of a given *ivec3* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: ivec3 getIVec3Arg ( const char * name ) const


Returns a value of a given *ivec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setIVec4Arg ( const char * name , const Math:: ivec4 & value )

Sets a value of a given *ivec4* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: ivec4 getIVec4Arg ( const char * name ) const


Returns a value of a given *ivec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setMat4Arg ( const char * name , const Math:: mat4 & value )

Sets a value of a given *mat4* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: mat4 getMat4Arg ( const char * name ) const


Returns a value of a given *mat4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## Ptr < Xml > getParent ( ) const

Returns the parent of the current XML node.
### Return value

XML node.
## bool setQuatArg ( const char * name , const Math:: quat & value )

Sets a value of a given *quat* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: quat getQuatArg ( const char * name ) const


Returns a value of a given *quat* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setRawData ( const char * data )

Sets a raw content for the node. Raw data will be automatically formatted as a CDATA section. This can be done only for nodes with no children.
### Arguments

- *const char ** **data** - Content to set.

### Return value

**1** if the content is set successfully; otherwise, **0**.
## bool setStringArrayArg ( const char * name , const Vector < String > & src )

Sets a vector of strings as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *const char ** **name** - Name of an argument.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **src** - An array of strings.

### Return value

Always **1**.
## bool getStringArrayArg ( const char * name , Vector < String > & OUT_dest ) const

Returns a set of string values stored in an argument and puts them in a vector.
### Arguments

- *const char ** **name** - Name of the string.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_dest** - Reference to a [*vector*](../../../code/uniginescript/language/containers/index.md#vector). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

**1** if *dest* contains anything; otherwise, **0**.
## bool setStringArrayData ( const Vector < String > & src , const char * delimiter = "," )

Sets a vector of strings as a content for the node. This can be done only for nodes with no children.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **src** - Reference to a [*vector*](../../../api/library/containers/vector/class.vector_cpp.md) of strings.
- *const char ** **delimiter** - Character(s) to be used as a delimiter to split tokens.

### Return value

true if the content is set successfully; otherwise, false.
## bool getStringArrayData ( Vector < String > & OUT_dest , const char * delimiter = "," ) const

Returns an interpretation of data stored in the node as a vector of strings.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_dest** - Reference to a [*vector*](../../../api/library/containers/vector/class.vector_cpp.md) of strings. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *const char ** **delimiter** - Character(s) to be used as a delimiter to split tokens.

### Return value

**1** if *dest* contains anything; otherwise, **0**.
## String getSubTree ( const char * path = 0 ) const

Dumps the node tree.
### Arguments

- *const char ** **path** - Path to XML sub-tree.

### Return value

Single-line non-indented output of the node tree. If no arguments are passed, the entire XML tree would be output.
## bool setVec2Arg ( const char * name , const Math:: vec2 & value )

Sets a value of a given *vec2* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: vec2 getVec2Arg ( const char * name ) const


Returns a value of a given *vec2* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setVec3Arg ( const char * name , const Math:: vec3 & value )

Sets a value of a given *vec3* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: vec3 getVec3Arg ( const char * name ) const


Returns a value of a given *vec3* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setVec4Arg ( const char * name , const Math:: vec4 & value )

Sets a value of a given *vec4* argument.
### Arguments

- *const char ** **name** - Name of an argument.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Value of an argument.

### Return value

Always **1**.
## Math:: vec4 getVec4Arg ( const char * name ) const


Returns a value of a given *vec4* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Name of a target argument.

### Return value

Argument value.
## bool setXmlData ( const char * data )

Sets an unquoted string to data stored in the node. This string can also contain XML sub-tree with rich text formatting.
### Arguments

- *const char ** **data** - Unquoted string to set.

### Return value

true if the string is set successfully; otherwise, false.
## Ptr < Xml > addChild ( const char * name , const char * args = 0 ) const

Appends a new XML node to the current XML node as a child.
### Arguments

- *const char ** **name** - Name of the XML node.
- *const char ** **args** - Arguments of the XML node. The default value is 0. > **Notice:** This value should be passed if the first argument is a string

### Return value

Created XML node.
## Ptr < Xml > addChild ( const Ptr < Xml > & xml ) const

Appends a new XML node to the current XML node as a child.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - XML sub-tree smart pointer.

### Return value

Created XML node.
## void clear ( )

Clears all data associated with the node.
## void clearChildren ( )

Clears all children of the current XML node.
## void clearUnusedData ( )

Clears the unused nodes and arguments.
## void copy ( const Ptr < Xml > & source )

Copies all data (name, arguments, data, flags and a child hierarchy) from the source XML node to the current one.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **source** - Source XML node.

## String decode ( const char * arg1 )

Decodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) and numeric character references.
### Arguments

- *const char ** **arg1** - Data to decode.

### Return value

Decoded string.
## String encode ( const char * arg1 )

Encodes special XML characters (less-than, greater-than, ampersand, double-quote and apostrophe) to their character entity reference.
### Arguments

- *const char ** **arg1** - Data to encode.

### Return value

Encoded string.
## Ptr < Xml > find ( const char * path ) const

Searches for an XML sub-tree.
### Arguments

- *const char ** **path** - Path to the XML sub-tree.

### Return value

Pointer to the XML node.
## int findArg ( const char * name ) const

Searches for a XML argument by its name.
### Arguments

- *const char ** **name** - XML argument name.

### Return value

XML argument number.
## int findChild ( const char * name ) const

Searches for the number of the XML node child by name.
### Arguments

- *const char ** **name** - Name of the XML node child.

### Return value

The number of the XML node child if it is exists; otherwise, -1.
## bool load ( const char * name , bool skip_errors = false )

Loads an XML document and sets the current node to be the root of the parsed tree.
### Arguments

- *const char ** **name** - File name.
- *bool* **skip_errors** - true to enable automatic skipping of errors (the file will be loaded in any case); false � to disable it (the file will not be loaded in case of any error).

### Return value

true if the file is read and parsed successfully; otherwise, false.
## bool load ( Ptr < Stream > & stream , size_t read_size , bool binary = false , bool skip_errors = false )

Loads XML data from the specified stream and sets the current node to be the root of the parsed tree.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream from which the data of the XML node is to be loaded.
- *size_t* **read_size** - Size of the data block to be read from the stream, in bytes.
- *bool* **binary** - Binary format flag: use true to load data in binary format, or false - to load it in text format.
- *bool* **skip_errors** - true to enable automatic skipping of errors (the data will be loaded in any case); false � to disable it (the data will not be loaded in case of any error).

### Return value

true if the data is read and parsed successfully; otherwise, false.
## bool parse ( const char * src )

Parses a string with XML mark-up and sets the current node to be the root of the parsed tree.
### Arguments

- *const char ** **src** - String pointer.

### Return value

true if a string is successfully parsed; otherwise false.
## void printUnusedData ( const char * name ) const

Logs warnings of unused data for debugging.
### Arguments

- *const char ** **name**

## int removeArg ( const char * name )

Removes the argument with the given name from the list of the current XML node arguments.
### Arguments

- *const char ** **name** - Name of the target argument.

### Return value

1 if the argument is deleted successfully; otherwise, 0.
## Ptr < Xml > removeChild ( const Ptr < Xml > & xml )

Removes a child node and its descendants from the current XML node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - XML sub-tree smart pointer.

### Return value

Removed child node and its descendants, if they are found; otherwise, 0.
## bool save ( const char * name , bool binary = false , const char * indent = "\t" ) const

Formats the tree of the current node and writes it to the specified file in the specified format. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *const char ** **name** - Path to the file.
- *bool* **binary** - Binary format flag: use true to save data to a binary file, or false - to save it to a text file.
- *const char ** **indent** - String to be used for indentation (e.g. "\t").

### Return value

true if the file is written successfully; otherwise, false.
## bool save ( Ptr < Stream > & stream , bool binary = false , const char * indent = "\t" ) const

Formats the tree of the current node and writes is to the specified stream in the specified format.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data of the XML node is to be written.
- *bool* **binary** - Binary format flag: use true to save data to a binary file, or false - to save it to a text file.
- *const char ** **indent** - String to be used for indentation (e.g. "\t").

### Return value

true if the file is written successfully; otherwise, false.
## String symbols ( const char * arg1 )

Replaces ampersand characters with character entity references.
### Arguments

- *const char ** **arg1** - String to encode.

### Return value

String which contains replaced ampersand characters with character entity references.
## bool setData ( const UGUID & guid )

Sets a UGUID content for the node.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( bool value )

Sets a boolean content for the node.
### Arguments

- *bool* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( int value , int radix = 10 )

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
## bool setData ( long long value )

Sets a long integer content for the node.
### Arguments

- *long long* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( float value )

Sets a float content for the node.
### Arguments

- *float* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( double value )

Sets a double content for the node.
### Arguments

- *double* **value**

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: vec2 & value )

Sets a vec2 vector content for the node.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: vec3 & value )

Sets a vec3 vector content for the node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: vec4 & value )

Sets a vec4 vector content for the node.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: dvec2 & value )

Sets a dvec2 vector content for the node.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: dvec3 & value )

Sets a dvec3 vector content for the node.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: dvec4 & value )

Sets a dvec4 vector content for the node.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: ivec3 & value )

Sets an ivec3 vector content for the node.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: ivec2 & value )

Sets an ivec2 vector content for the node.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: ivec4 & value )

Sets an ivec4 vector content for the node.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: mat4 & value )

Sets a mat4 matrix content for the node.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: dmat4 & value )

Sets a dmat4 matrix content for the node.
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Math:: quat & value )

Sets a quaternion content for the node.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## bool setData ( const Palette & value )

Sets a palette content for the node.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **value** - Content to set.

### Return value

true if the content is set successfully; otherwise, false.
## void readChildData ( const char * name , bool & value ) const

Reads a boolean interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *bool &* **value** - Target boolean variable.

## void readChildData ( const char * name , int & value ) const

Reads an integer interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *int &* **value** - Target integer variable.

## void readChildData ( const char * name , char & value ) const

Reads a character interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *char &* **value** - Target character variable.

## void readChildData ( const char * name , long long & value ) const

Reads a long integer interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *long long &* **value** - Target long integer variable.

## void readChildData ( const char * name , float & value ) const

Reads a float interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *float &* **value** - Target float variable.

## void readChildData ( const char * name , double & value ) const

Reads a double interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *double &* **value** - Target double variable.

## void readChildData ( const char * name , Math:: vec2 & value ) const

Reads a vec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Target vec2 variable.

## void readChildData ( const char * name , Math:: vec3 & value ) const

Reads a vec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Target vec3 variable.

## void readChildData ( const char * name , Math:: vec4 & value ) const

Reads a vec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Target vec4 variable.

## void readChildData ( const char * name , Math:: dvec2 & value ) const

Reads a dvec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Target dvec2 variable.

## void readChildData ( const char * name , Math:: dvec3 & value ) const

Reads a dvec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Target dvec3 variable.

## void readChildData ( const char * name , Math:: dvec4 & value ) const

Reads a dvec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Target dvec4 variable.

## void readChildData ( const char * name , Math:: ivec2 & value ) const

Reads an ivec2 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Target ivec2 variable.

## void readChildData ( const char * name , Math:: ivec3 & value ) const

Reads an ivec3 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Target ivec3 variable.

## void readChildData ( const char * name , Math:: ivec4 & value ) const

Reads an ivec4 vector interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Target ivec4 variable.

## void readChildData ( const char * name , Math:: mat4 & value ) const

Reads a mat4 matrix interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Target mat4 variable.

## void readChildData ( const char * name , Math:: dmat4 & value ) const

Reads a dmat4 matrix interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Target dmat4 variable.

## void readChildData ( const char * name , Palette & value ) const

Reads a palette interpretation of the data stored in the node with the specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Child node name.
- *[Palette](../../../api/library/common/class.palette_cpp.md) &* **value** - Target palette variable.

## void readArg ( const char * name , bool & value ) const

Reads a boolean interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *bool &* **value** - Target boolean variable.

## void readArg ( const char * name , int & value ) const

Reads an integer interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *int &* **value** - Target integer variable.

## void readArg ( const char * name , char & value ) const

Reads a character interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *char &* **value** - Target character variable.

## void readArg ( const char * name , float & value ) const

Reads a float interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *float &* **value** - Target float variable.

## void readArg ( const char * name , double & value ) const

Reads a double interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *double &* **value** - Target double variable.

## void readArg ( const char * name , Math:: vec2 & value ) const

Reads a vec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Target vec2 variable.

## void readArg ( const char * name , Math:: vec3 & value ) const

Reads a vec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Target vec3 variable.

## void readArg ( const char * name , Math:: vec4 & value ) const

Reads a vec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Target vec4 variable.

## void readArg ( const char * name , Math:: dvec2 & value ) const

Reads a dvec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Target dvec2 variable.

## void readArg ( const char * name , Math:: dvec3 & value ) const

Reads a dvec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Target dvec3 variable

## void readArg ( const char * name , Math:: dvec4 & value ) const

Reads a dvec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Target dvec4 variable.

## void readArg ( const char * name , Math:: ivec2 & value ) const

Reads a ivec2 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Target ivec2 variable.

## void readArg ( const char * name , Math:: ivec3 & value ) const

Reads a ivec3 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Target ivec3 variable.

## void readArg ( const char * name , Math:: ivec4 & value ) const

Reads a ivec4 interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Target ivec4 variable.

## void readArg ( const char * name , Palette & value ) const

Reads a *palette* interpretation of the argument in the node with specified name and puts it to the specified target variable.
### Arguments

- *const char ** **name** - Name of the target argument.
- *[Palette](../../../api/library/common/class.palette_cpp.md) &* **value** - Target palette variable.

## bool setPaletteArg ( const char * name , const Palette & value )

Sets a *palette* value of a given argument.
### Arguments

- *const char ** **name** - The argument name.
- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **value** - The argument value.

### Return value

Always **1**.
## Palette getPaletteArg ( const char * name ) const

Returns a *palette* value of a specified argument.
### Arguments

- *const char ** **name** - The argument name.

### Return value

Value of the argument, if it is found; otherwise, **0**.
## void setPaletteData ( const Palette & data )

Sets a *palette* content for the node. This can be done only for nodes with no children.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **data** - Content to set.

## Palette getPaletteData ( ) const

Returns a *palette* interpretation of data stored in the node.
### Return value

Data stored in the node.
## bool setLongArg ( const char * name , long long value , int radix = 10 )

Sets a *long* value of a given argument.
### Arguments

- *const char ** **name** - The argument name.
- *long long* **value** - The argument value.
- *int* **radix** - Radix (base) specifying the form of representation of the value, one of the following:

  - 2 - binary
  - 8 - octal
  - 10 - decimal (default)
  - 16 - hexadecimal

### Return value

Always **1**.
## long long getLongArg ( const char * name ) const


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - The argument name.

### Return value

The argument value.
## long long getLongArg ( const char * name , long long value ) const


Returns a value of a given *long* argument.


> **Notice:** To check if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - The argument name.
- *long long* **value** - Default value of the argument.

### Return value

The argument value.
## bool setLongArrayArg ( const char * name , llong[] src , int radix = 10 )

Sets the specified array of *long* elements as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *const char ** **name** - The argument name.
- *llong[]* **src** - An array of long values.
- *int* **radix** - Radix (base) specifying the form of representation of the value, one of the following:

  - 2 - binary
  - 8 - octal
  - 10 - decimal (default)
  - 16 - hexadecimal

### Return value

true if the array is set successfully; otherwise, false.
## bool getLongArrayArg ( const char * name , const llong* dest , int dest_size ) const

Retrieves a set of *long* values stored in an argument and puts them to the specified array.
### Arguments

- *const char ** **name** - Name of a target argument.
- *const llong** **dest** - Target array with *llong* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
## bool setIntArrayArg ( const char * name , int[] src , int radix = 10 )

Sets the specified array of *int* elements as a value of a given argument in a given number notation. By default, the decimal number notation is used.
### Arguments

- *const char ** **name** - Name of an argument.
- *int[]* **src** - An array of integers.
- *int* **radix** - Radix to use when setting a value.

### Return value

true if the array is set successfully; otherwise, false.
## bool getIntArrayArg ( const char * name , const int* dest , int dest_size ) const

Retrieves a set of *int* values stored in an argument and puts them to the specified array.
### Arguments

- *const char ** **name** - Name of a target argument.
- *const int** **dest** - Target array with *int* elements.
- *int* **dest_size** - Array size.

### Return value

true if *dest* contains anything; otherwise, false.
