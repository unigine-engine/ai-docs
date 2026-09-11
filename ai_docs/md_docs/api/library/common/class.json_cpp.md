# Unigine::Json Class (CPP)

**Header:** #include <UnigineJson.h>


This class is used to parse and create JSON formatted strings.


Each Json node has a type, a name, and a value. The following types are available:


- null
- bool
- number
- string
- array
- object


The Json node has a hierarchy structure: it can have child Json nodes and a parent node.


#### Creating a Json Node


The following code creates a Json node, adds child nodes with different types of values and saves the result to a `*.json` file:


> **Notice:** When you add the *array*/*object* child nodes, you must call the *[setArray()](#setArray_void)/[setObject()](#setObject_void)* functions after *addChild()*.


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	JsonPtr json = Json::create();

	json->addChild("child_0", 0);    // int
	json->addChild("child_1", 1.1);   // float
	json->addChild("child_2", "two");  // string

	// array
	JsonPtr array_0 = json->addChild("array_0");
	array_0->setArray();
	array_0->addChild(NULL, 1);
	array_0->addChild(NULL, 1);
	array_0->addChild(NULL, 0);

	// object
	JsonPtr object_0 = json->addChild("object_0");
	object_0->setObject();
	object_0->addChild("one", 5);
	object_0->addChild("two", 6);
	object_0->addChild("three", 7);

	// save the Json node to the file
	json->save("json/my.json");

	return 1;
}


```


`my.json`:


```text
{
	"child_0": 0,
	"child_1": 1.1000000000000001,
	"child_2": "two",
	"array_0": [
		1,
		1,
		0
	],
	"object_0": {
		"one": 5,
		"two": 6,
		"three": 7
	}
}

```


Child nodes have names *child_0*, *child_1*, *child_2* and values: integer 0, double 1.1 and string two. There are also *array_0* and *object_0* child nodes of the array and object types respectively. The name of the child node always has the string type.


#### Editing a Json Node


A Json node can be edited by means of the Json class: you can add or remove child nodes, change its values. For example, to add a new array node, you can do the following:


`my_array.json`


```text
{
"array_0": [ 0, 0, 1 ]
}

```


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	JsonPtr json = Json::create();

	// load the Json node from my.json
	json->load("json/my_array.json");

	// add the array node as a child
	JsonPtr array_1 = json->addChild("array_1");
	array_1->setArray();
	// add object nodes to the array
	for (int i = 0; i < 5; i++)
	{
		JsonPtr object = array_1->addChild(NULL);
		object->addChild("name", String::format("value_%d", i));
		object->addChild("value", i + 1);
	}

	// save the updated Json node to a new file
	json->save("json/my_array.json");

	return 1;
}


```


The result:


```text
{
"array_0": [ 0, 0, 1 ],
"array_1": [
	{
		"name": "value_0",
		"value": 1
	},
	{
		"name": "value_1",
		"value": 2
	},
	{
		"name": "value_2",
		"value": 3
	},
	{
		"name": "value_3",
		"value": 4
	},
	{
		"name": "value_4",
		"value": 5
	}
]
}

```


You can also change the type of the node. However, in some cases, this can lead to data loss. For example, if you change the type from *object* to *array*, names of the child nodes will be lost.


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	JsonPtr json = Json::create();

	// create an object node
	JsonPtr object_0 = json->addChild("array_or_object?");
	object_0->setObject();
	object_0->addChild("name1", 1);
	object_0->addChild("name2", 2);
	object_0->addChild("name3", 3);
	// save to a file
	json->save("json/object.json");
	// change the type to "array"
	object_0->setArray();
	// save to another file
	json->save("json/array.json");

	return 1;
}


```


In the result, the files will contain the following:


`object.json`


```text
{
	"array_or_object?": {
		"name1": 1,
		"name2": 2,
		"name3": 3
	}
}

```


`array.json`


```text
{
	"array_or_object?": [
		1,
		2,
		3
	]
}

```


##### Accessing Data


The Json class provides several methods for accessing data of a Json node depending of its type. For example, you can use the *[read()](#read_cstr_bool_void)* methods to access data of the *object* Json node as follows:


`cubes.json`


```text
{
	"cubes": {
		"first": {
			"name": "cube_red",
			"coefficient": 1.0
			"color": [255, 0, 0, 255]
		},
		"second": {
			"name": "cube_green",
			"coefficient": 2.0
			"color": [0, 255, 0, 255]
		},
		"third": {
			"name": "cube_blue",
			"coefficient": 3.0
			"color": [0, 0, 255, 255]
		},
		"fourth": {
			"name": "cube_magenta",
			"coefficient": 4.0
			"color": [255, 0, 255, 255]
		},
		"fifth": {
			"name": "cube_white",
			"coefficient": 5.0
			"color": [255, 255, 255, 255]
		}
	}
}

```


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	float coefficient;
	String name;
	vec4 color;

	JsonPtr json = Json::create();

	// load the Json node from the file
	json->load("json/cubes.json");
	// get its child node
	JsonPtr cubes = json->getChild("cubes");

	for (int i = 0; i < cubes->getNumChildren(); i++)
	{
		// get a child node of the "cubes" node
		JsonPtr child = cubes->getChild(i);

		// read the node name
		name = child->read("name");
		// read the coefficient to a variable
		child->read("coefficient", coefficient);
		// read the color to a variable
		child->read("color", color);

		// create a dynamic mesh using read values
		ObjectMeshDynamicPtr box = Primitives::createBox(Math::vec3_one * coefficient);
		box->setName(name);
		box->setWorldPosition(Math::Vec3(0.0f, 0.0f, 1.0f * coefficient));
		box->setMaterialParameterFloat4("albedo_color", color, 0);
		Log::message("The %s box: %s\n", child->getName(), box->getName());

	}

	return 1;
}


```


In the result, five colored cubes will be created by using data from the provided `cubes.json` file.


If you have an *array* of two, three or four elements, you can use the *[getVec2()](#getVec2_vec2)*, *[getVec3()](#getVec3_vec3)* and *[getVec4()](#getVec4_vec4)* methods correspondingly. For example:


`my_array.json`


```text
{
	"array_0": [ 0, 0, 1 ]
}

```


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	// get the "array_0" child
	JsonPtr a = json->getChild("array_0");
	// get its value
	vec3 v = a->getVec3();
	// print the result to the console
	Log::message("%f %f %f\n", v.x, v.y, v.z);

	return 1;
}


```


By using the *write()* methods of the class, you can also add a new child nodes and edit values of the existing ones. For example:


```cpp
#include <UnigineJson.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{

	json->load("json/cubes.json");

	// add a new child node of the object type
	JsonPtr cube = json->getChild("cubes")->addChild("sixth");
	cube->setObject();
	// write new child nodes with the specified values
	cube->write("name", "cube_black");
	cube->write("coefficient", 6.0);
	cube->write("color", vec4(0, 0, 0, 0));

	// write new values for the existing Json node
	cube = json->getChild("cubes")->getChild("first");
	cube->write("name", "cube_black");
	cube->write("coefficient", 3.0);
	cube->write("color", vec4(0, 0, 0, 0));

	// save changes to the .json file
	json->save("json/cubes.json");

	return 1;
}


```


## Json Class

---

## static JsonPtr create ( )

Default constructor that creates an empty instance.
## static JsonPtr create ( const char * name )

Constructor that creates a JSON node with a given name.
### Arguments

- *const char ** **name** - Name of the Json node.

## void setArray ( )


Sets the array type to the current Json node.


> **Notice:** This method can be called for a newly added node or for the existing node to change its type. However, in certain cases, this can lead to data loss. For example, if you change the type from *object* to *array*, names of the child nodes will be lost.


## int isArray ( ) const

Returns a value indicating if the Json node has an array type.
### Return value

1 if the Json has an array type; otherwise, 0.
## void setBool ( int arg1 )

Sets a boolean value and type to the current Json node.
### Arguments

- *int* **arg1** - Integer value.

## int getBool ( ) const

Reads a boolean value of the current Json node.
### Return value

1 if the Json node has a bool type; otherwise, 0.
## int isBool ( ) const

Returns a value indicating if the Json node has a bool type.
### Return value

1 if the Json has a bool type; otherwise, 0.
## Ptr < Json > getChild ( int num ) const

Returns the child node of the current Json node by the child number.
### Arguments

- *int* **num** - Number of the child of the Json node.

### Return value

Child Json node.
## Ptr < Json > getChild ( const char * name ) const

Returns the child node of the current Json node by the child name.
### Arguments

- *const char ** **name** - Name of the Json node.

### Return value

Child Json node.
## int isChild ( const char * name ) const

Checks if a child node with a given name exists.
### Arguments

- *const char ** **name** - Name of the child node.

### Return value

1 if a child with the provided name exists; otherwise, 0.
## Ptr < Json > addChild ( const char * name , double value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *const char ** **name** - Node name.
- *double* **value** - Node value.

### Return value

Child Json node.
## Ptr < Json > addChild ( const char * name , int value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *const char ** **name** - Node name.
- *int* **value** - Node value.

### Return value

Child Json node.
## Ptr < Json > addChild ( const char * name , const char * value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *const char ** **name** - Node name.
- *const char ** **value** - Node value.

### Return value

Child Json node.
## Ptr < Json > addChild ( const char * name )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *const char ** **name** - Node name.

### Return value

Child Json node.
## Ptr < Json > addChild ( const Ptr < Json > & json )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - Node name.

### Return value

Child Json node.
## Ptr < Json > addChild ( )

Adds a child node to the current Json node.
### Return value

Child Json node.
## String getSubTree ( const char * name = 0 )

Returns a subtree of a Json node as the non-formatted string.
### Arguments

- *const char ** **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Non-formatted subtree.
## String getFormattedSubTree ( const char * name = 0 )

Returns a subtree of a Json node as the formatted string.
### Arguments

- *const char ** **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Formatted subtree.
## void setName ( const char * name )

Sets the given name to the Json node.
### Arguments

- *const char ** **name** - Name of the Json node.

## const char * getName ( ) const

Returns the name of the current Json node.
### Return value

The name of the Json node.
## void setNull ( )

Sets null type to the current Json node.
## int isNull ( ) const

Returns a value indicating if the Json node has a null type.
### Return value

1 if the Json has a null type; otherwise, 0.
## void setNumber ( double arg1 )

Sets a number value and type to the current Json node.
### Arguments

- *double* **arg1** - Double value.

## double getNumber ( ) const

Returns the number value of the current Json node.
### Return value

Number value of the current Json node.
## int isNumber ( ) const

Returns a value indicating if the Json node has a number type.
### Return value

1 if the Json has a number type; otherwise, 0.
## int getNumChildren ( ) const

Returns the number of child nodes of the current Json node.
### Return value

Number of child nodes.
## void reserveChildren ( int num )

Sets the reserved capacity of the Json node to store the specified number of child nodes.
### Arguments

- *int* **num** - Number of child nodes.

## void setObject ( )

Sets object type to the current Json node.
## int isObject ( ) const

Returns a value indicating if the Json node has an *object* type.
### Return value

1 if the Json has an *object* type; otherwise, 0.
## Ptr < Json > getParent ( )

Returns the parent node of the current Json node.
### Return value

Parent Json node.
## void setString ( const char * arg1 )

Sets a string value and type to the current Json node. The function automatically casts number values to string type.
### Arguments

- *const char ** **arg1** - String value.

## const char * getString ( ) const

Returns the string value stored in this JSON node. Valid only when the node actually holds a string (**[isString()](../../...md#isString_int)** returns true).
### Return value

String value of the current Json node.
## int isString ( ) const

Returns a value indicating if the Json node has a string type.
### Return value

1 if the Json has a string type; otherwise, 0.
## void clear ( )

Clears all data of the current Json node including type, value, name and all children. If the current Json node has a parent, it also removed from the parent Json node.
## Ptr < Json > removeChild ( const Ptr < Json > & json )

Removes the child Json node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - Json node to be removed.

### Return value

Removed child Json node.
## Ptr < Json > removeChild ( const char * name )

Removes the child Json node.
### Arguments

- *const char ** **name** - Name of the Json node to be removed.

### Return value

Removed child Json node.
## void clearChildren ( )

Clears all children of the current Json node.
## void copy ( const Ptr < Json > & source )

Copies type, name and value from the source Json node to the current Json node and adds the source Json child nodes as child nodes to the current Json node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **source** - Source Json node.

## Ptr < Json > find ( const char * name )

Finds Json node by its name in current Json node tree.
### Arguments

- *const char ** **name** - Name of the Json node.

### Return value

Founded Json node.
## int load ( const char * path )

Loads the data to the current Json node from the file with a given path.
### Arguments

- *const char ** **path** - Path of the file.

### Return value

1 if the Json node was loaded successfully; otherwise, 0.
## int parse ( const char * source )

Parses a given string into the Json node.


**Usage Example**


```cpp
#include <UnigineJson.h>

/* ... */

JsonPtr json = Json::create();
json->addChild("child_0", 1);

JsonPtr json_2 = Json::create();
json_2->parse(json->getSubTree().get());

```


Now the json_2 node contains:


```text
{
	"child_0": 1
}

```


### Arguments

- *const char ** **source** - String to parse.

### Return value

1 if the string was parsed successfully; otherwise, 0.
## int save ( const char * path ) const

Saves the Json node into a file with a given path. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *const char ** **path** - Path to the file.

### Return value

1 if the file was saved successfully; otherwise, 0.
## void read ( const char * name , bool & value ) const

Reads a boolean value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *bool &* **value** - Target boolean variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , int & value ) const

Reads an integer value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *int &* **value** - Target integer variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , unsigned int & value ) const

Reads an unsigned integer value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *unsigned int &* **value** - Target unsigned integer variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , char & value ) const

Reads a character value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *char &* **value** - Target character variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , double & value ) const

Reads a double value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *double &* **value** - Target double variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , float & value ) const

Reads a float value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *float &* **value** - Target float variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , UGUID & value ) const

Reads a value of a Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - UGUID of the variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: vec2 & value ) const

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: vec3 & value ) const

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: vec4 & value ) const

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: dvec2 & value ) const

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: dvec3 & value ) const

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: dvec4 & value ) const

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: ivec2 & value ) const

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: ivec3 & value ) const

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Math:: ivec4 & value ) const

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void read ( const char * name , Vector < int > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < char > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< char > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < double > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< double > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < float > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< float > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < String > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: vec2 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: vec3 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: vec4 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: dvec2 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: dvec3 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: dvec4 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: ivec2 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: ivec3 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( const char * name , Vector < Math:: ivec4 > & OUT_value ) const

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *const char ** **name** - Name of the Json node.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( bool & value ) const

Reads a boolean value of the Json node to the specified target variable.
### Arguments

- *bool &* **value** - Target boolean variable to which the value of the Json node is saved.

## void read ( int & value ) const

Reads an integer value of the Json node to the specified target variable.
### Arguments

- *int &* **value** - Target integer variable to which the value of the Json node is saved.

## void read ( char & value ) const

Reads a character value of the Json node to the specified target variable.
### Arguments

- *char &* **value** - Target character variable to which the value of the Json node is saved.

## void read ( double & value ) const

Reads a double value of the Json node to the specified target variable.
### Arguments

- *double &* **value** - Target double variable to which the value of the Json node is saved.

## void read ( float & value ) const

Reads a float value of the Json node to the specified target variable.
### Arguments

- *float &* **value** - Target float variable to which the value of the Json node is saved.

## void read ( Math:: vec2 & value ) const

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void read ( Math:: vec3 & value ) const

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void read ( Math:: vec4 & value ) const

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void read ( Math:: dvec2 & value ) const

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void read ( Math:: dvec3 & value ) const

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void read ( Math:: dvec4 & value ) const

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void read ( Math:: ivec2 & value ) const

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void read ( Math:: ivec3 & value ) const

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void read ( Math:: ivec4 & value ) const

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void read ( Vector < bool > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< bool > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < int > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < char > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< char > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < double > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< double > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < float > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< float > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < String > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: vec2 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: vec3 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: vec4 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: dvec2 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: dvec3 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: dvec4 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: ivec2 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: ivec3 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void read ( Vector < Math:: ivec4 > & OUT_value ) const

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) > &* **OUT_value** - Vector to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## String read ( const char * name ) const

Returns a value of a Json node with the specified name as a string.
### Arguments

- *const char ** **name** - Name of the Json node.

### Return value

Node value.
## void write ( const char * name , bool value )

Writes the specified boolean value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *bool* **value** - Boolean value to be written to the Json node with the specified name.

## void write ( const char * name , int value )

Writes the specified integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *int* **value** - Integer value to be written to the Json node with the specified name.

## void write ( const char * name , unsigned int value )

Writes the specified unsigned integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *unsigned int* **value** - Unsigned integer value to be written to the Json node with the specified name.

## void write ( const char * name , char value )

Writes the specified character value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *char* **value** - Character value to be written to the Json node with the specified name.

## void write ( const char * name , const char * value )

Writes the specified value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const char ** **value** - Value to be written to the Json node with the specified name.

## void write ( const char * name , double value )

Writes the specified double value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *double* **value** - Double value to be written to the Json node with the specified name.

## void write ( const char * name , float value )

Writes the specified float value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *float* **value** - Float value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: vec2 & value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Two-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: vec3 & value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Three-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: vec4 & value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Four-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: dvec2 & value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Two-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: dvec3 & value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Three-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: dvec4 & value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Four-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: ivec2 & value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Two-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: ivec3 & value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Three-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Math:: ivec4 & value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Four-component value to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < int > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < char > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< char > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < double > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< double > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < float > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< float > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < String > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: vec2 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: vec3 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: vec4 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: dvec2 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: dvec3 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: dvec4 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: ivec2 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: ivec3 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const Vector < Math:: ivec4 > & value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) > &* **value** - Vector of values to be written to the Json node with the specified name.

## void write ( const char * name , const UGUID& value )

Writes the specified value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *const UGUID&* **value** - UGUID of the value to be written to the Json node with the specified name.

## void write ( const UGUID& value )

Writes the specified value to the current Json node.
### Arguments

- *const UGUID&* **value** - UGUID of the value to be written to the Json node.

## void write ( bool value )

Writes the specified boolean value to the current Json node.
### Arguments

- *bool* **value** - Boolean value to be written to the current Json node.

## void write ( int value )

Writes the specified integer value to the current Json node.
### Arguments

- *int* **value** - Integer value to be written to the current Json node.

## void write ( char value )

Writes the specified character value to the current Json node.
### Arguments

- *char* **value** - Character value to be written to the current Json node.

## void write ( const char * value )

Writes the specified value to the current Json node.
### Arguments

- *const char ** **value** - Value to be written to the current Json node.

## void write ( double value )

Writes the specified double value to the current Json node.
### Arguments

- *double* **value** - Double value to be written to the current Json node.

## void write ( float value )

Writes the specified float value to the current Json node.
### Arguments

- *float* **value** - Float value to be written to the current Json node.

## void write ( const Math:: vec2 & value )

Writes the specified two-component value to the current Json node.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Two-component value to be written to the current Json node.

## void write ( const Math:: vec3 & value )

Writes the specified three-component value to the current Json node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Three-component value to be written to the current Json node.

## void write ( const Math:: vec4 & value )

Writes the specified four-component value to the current Json node.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Four-component value to be written to the current Json node.

## void write ( const Math:: dvec2 & value )

Writes the specified two-component value to the current Json node.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Two-component value to be written to the current Json node.

## void write ( const Math:: dvec3 & value )

Writes the specified three-component value to the current Json node.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Three-component value to be written to the current Json node.

## void write ( const Math:: dvec4 & value )

Writes the specified four-component value to the current Json node.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Four-component value to be written to the current Json node.

## void write ( const Math:: ivec2 & value )

Writes the specified two-component value to the current Json node.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Two-component value to be written to the current Json node.

## void write ( const Math:: ivec3 & value )

Writes the specified three-component value to the current Json node.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Three-component value to be written to the current Json node.

## void write ( const Math:: ivec4 & value )

Writes the specified four-component value to the current Json node.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Four-component value to be written to the current Json node.

## void write ( const Vector < bool > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< bool > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < int > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < char > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< char > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < double > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< double > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < float > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< float > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < String > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: vec2 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: vec3 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: vec4 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: dvec2 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: dvec3 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: dvec4 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: ivec2 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: ivec3 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## void write ( const Vector < Math:: ivec4 > & value )

Writes the specified values to the current Json node.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) > &* **value** - Vector of values to be written to the current Json node.

## const char * getTypeName ( ) const

Returns the name of the [type](#node_type) of the Json node.
### Return value

Name of the Json node type.
## void setInt ( int value )

Sets the specified integer value to the current Json node.
### Arguments

- *int* **value** - Value to be set to the current Json node.

## void setInt ( const char * name , int value )

Sets the specified integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *const char ** **name** - Name of the target Json node.
- *int* **value** - Value to be set to the target Json node.

## int getInt ( ) const

Returns the value of the current Json node as an integer value, if possible.
### Return value

Node value.
## int getInt ( const char * name ) const

Returns the value of the target Json node with the specified name as an integer value, if possible.
### Arguments

- *const char ** **name** - Name of the target Json node.

## void setVec2 ( const Math:: vec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Vector setting the first two elements of the array-type Json node.

## Math:: vec2 getVec2 ( ) const

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setVec3 ( const Math:: vec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Vector setting the first three elements of the array-type Json node.

## Math:: vec3 getVec3 ( ) const

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setVec4 ( const Math:: vec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Vector setting the first four elements of the array-type Json node.

## Math:: vec4 getVec4 ( ) const

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void setDVec2 ( const Math:: dvec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Vector setting the first two elements of the array-type Json node.

## Math:: dvec2 getDVec2 ( ) const

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0, 0.0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setDVec3 ( const Math:: dvec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Vector setting the first three elements of the array-type Json node.

## Math:: dvec3 getDVec3 ( ) const

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setDVec4 ( const Math:: dvec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Vector setting the first four elements of the array-type Json node.

## Math:: dvec4 getDVec4 ( ) const

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void setIVec2 ( const Math:: ivec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Vector setting the first two elements of the array-type Json node.

## Math:: ivec2 getIVec2 ( ) const

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array a zero-vector (0, 0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setIVec3 ( const Math:: ivec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Vector setting the first three elements of the array-type Json node.

## Math:: ivec3 getIVec3 ( ) const

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setIVec4 ( const Math:: ivec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Vector setting the first four elements of the array-type Json node.

## Math:: ivec4 getIVec4 ( ) const

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0, 0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
