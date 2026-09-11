# Unigine::Json Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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
Json json = new Json();
json.addChild("child_0",0);    // int
json.addChild("child_1",1.1);   // float
json.addChild("child_2","two");   // string

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


In the result, five colored cubes will be created by using data from the provided `cubes.json` file.


If you have an *array* of two, three or four elements, you can use the *[getVec2()](#getVec2_vec2)*, *[getVec3()](#getVec3_vec3)* and *[getVec4()](#getVec4_vec4)* methods correspondingly. For example:


`my_array.json`


```text
{
	"array_0": [ 0, 0, 1 ]
}

```


By using the *write()* methods of the class, you can also add a new child nodes and edit values of the existing ones. For example:


## Json Class

---

## static Json ( )

Default constructor that creates an empty instance.
## static Json ( string name )

Constructor that creates a JSON node with a given name.
### Arguments

- *string* **name** - Name of the Json node.

## void setArray ( )

Sets array type to the current Json node and adds a given array as a child.
**Usage Example**


**Adding an Array**


The following example shows how to add an array to the Json node.


```cpp
Json json = new Json();
Json array = json.addChild("array");
array.setArray((1,2.2,"3"));
array.addChild(NULL,"data_0");
array.addChild(NULL, 5);

```


The result is:


```text
{
	"array": [
	1,
	2.2,
	"3",
	"data_0",
	5
	]
}

```


**Adding an Array to Array**


To add array to the array, just add an array as a child:


```cpp
Json json = new Json();
Json array = json.addChild("array");
array.setArray((1,2.2,"3"));
array.addChild(NULL,"data_0");
array.addChild(NULL, 5);
array.addChild(NULL,"array").setArray((5,6,7));

```


The result is:


```text
{
	"array": [
		1,
		2.2,
		"3",
		"data_0",
		5",
	[
		5,
		6,
		7
	]
	]
}

```


**Adding an Object to Array**


To add an object to array, do the following:


```cpp
Json json = new Json();
Json array = json.addChild("array");
array.setArray((1,2.2,"3"));
array.addChild(NULL,"object").setObject(("one": 5, "two": 6, "three": 7));

```


The result is:


```text
{
	"array": [
		1,
		2.2,
		"3",
	{
		"one": 5,
		"three": 7,
		"two": 6
	}
	]
}

```


> **Notice:** The *setObject()* function alphabetizes child nodes by using their names.


## int isArray ( )

Returns a value indicating if the Json node has an array type.
### Return value

1 if the Json has an array type; otherwise, 0.
## void setBool ( variable var , int arg1 )

Sets a boolean value and type to the current Json node.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *string* value - all strings except "true", set "false".
  - *int* value - all int values except 0, set "true".
  - *double* value - all double values except 0.0, set "true".
  - *float* value - all float values except 0.0f, set "true".
- *int* **arg1** - Integer value.

## int getBool ( )

Reads a boolean value of the current Json node.
### Return value

1 if the Json node has a bool type; otherwise, 0.
## int isBool ( )

Returns a value indicating if the Json node has a bool type.
### Return value

1 if the Json has a bool type; otherwise, 0.
## getChild ( int num , variable var )

Returns the child node of the current Json node.
### Arguments

- *int* **num** - Number of the child of the Json node.
- *variable* **var** - Argument of one of the following types:

  - *string* name - Name of the Json node.
  - *int* number - Number of the child of the Json node.

### Return value

Child Json node.
## int isChild ( string name )

Checks if a child node with a given name exists.
### Arguments

- *string* **name** - Name of the child node.

### Return value

1 if a child with the provided name exists; otherwise, 0.
## addChild ( variable var )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *Json* json - Json node.
  - *string* name - Name of the Json node.

### Return value

Child Json node.
## addChild ( variable var )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *Json* json - Json node.
  - *string* name - Name of the Json node.

### Return value

Child Json node.
## String getSubTree ( string name = 0 )

Returns a subtree of a Json node as the non-formatted string.


**Usage Example**


To get the subtree of a Json node, do the following:


```cpp
Json json = new Json();

json.addChild("child_0", 1);
json.addChild("child_1", 2.2);
json.addChild("child_2", "three");
Json object = json.addChild("object");
object.setObject(("1": 5, "4": 6, "2": 7));

string subTree = json.getSubTree();
log.message("the subtree is:%s\n", subTree);

```


In the console you see the following:


```text
the subtree is:{"child_0":1,"child_1":2.2,"child_2":"three","object":{"1":5,"2":7,"4":6}}
```


### Arguments

- *string* **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Non-formatted subtree.
## String getFormattedSubTree ( string name = 0 )

Returns a subtree of a Json node as the formatted string.


**Usage Example**


To get the formatted subtree of a Json node, do the following:


```cpp
Json json = new Json();

json.addChild("child_0", 1);
json.addChild("child_1", 2.2);
json.addChild("child_2", "three");
Json object = json.addChild("object");
object.setObject(("1": 5, "4": 6, "2": 7));

string fSubTree = json.getFormattedSubTree();
log.message("the formatted subtree is:%s\n", fSubTree);

```


In the console you see the following:


```text
the formatted subtree is:{
	"child_0": 1,
	"child_1": 2.2,
	"child_2": "three",
	"object": {
	"1": 5,
	"2": 7,
	"4": 6
	}
}

```


### Arguments

- *string* **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Formatted subtree.
## void setName ( string name )

Sets the given name to the Json node.
### Arguments

- *string* **name** - Name of the Json node.

## string getName ( )

Returns the name of the current Json node.
### Return value

The name of the Json node.
## void setNull ( )

Sets null type to the current Json node.
## int isNull ( )

Returns a value indicating if the Json node has a null type.
### Return value

1 if the Json has a null type; otherwise, 0.
## void setNumber ( variable var , double arg1 )

Sets a number value and type to the current Json node.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *int* number - integer value. For example, 5.
  - *double* number - double value. For example, 5.0.
  - *float* number - float value. For example, 5.0f.
  - *string* value - string with value. For example, "5".
- *double* **arg1** - Double value.

## double getNumber ( )

Returns the number value of the current Json node.
### Return value

Number value of the current Json node.
## int isNumber ( )

Returns a value indicating if the Json node has a number type.
### Return value

1 if the Json has a number type; otherwise, 0.
## int getNumChildren ( )

Returns the number of child nodes of the current Json node.
### Return value

Number of child nodes.
## void reserveChildren ( int num )

Sets the reserved capacity of the Json node to store the specified number of child nodes.
### Arguments

- *int* **num** - Number of child nodes.

## void setObject ( )

Sets object type to the current Json node and adds a given object as a child.


**Usage Example**


**Adding an Object**


To add an object to the Json node, do the following:


```cpp
Json json = new Json();
Json object = json.addChild("object");
object.setObject(("1": 5, "4": 6, "2": 7, "3": 8));
object.addChild("child_0", "data_0");

```


The result is:


```text
{
	"object": {
		"1": 5,
		"2": 7,
		"3": 8,
		"4": 6,
		"child_0": "data_0"
	}
}

```


> **Notice:** The *setObject()* function alphabetizes child nodes by using their names.


**Adding an Array to the Object**


To add an array to the added object, do the following:


```cpp
Json json = new Json();
Json object = json.addChild("object");
object.setObject(("1": 5, "4": 6, "2": 7, "3": 8));
object.addChild(class_remove(new Json("array"))).setArray((1,2,3));

```


The result is:


```text
{
	"object": {
		"1": 5,
		"2": 7,
		"3": 8,
		"4": 6,
		"array": [
			1,
			2,
			3
		]
	}
}

```


**Adding an Object to the Object**


To add an object to the added object, do the following:


```cpp
Json json = new Json();
Json object = json.addChild("object");
object.setObject(("1": 5, "4": 6, "2": 7, "3": 8));
object.addChild(class_remove(new Json("object"))).setObject(("one" : 1,"two" : 2,"three" : 3));

```


The result is:


```text
{
	"object": {
		"1": 5,
		"2": 7,
		"3": 8,
		"4": 6,
		"object": {
			"one": 1,
			"three": 3,
			"two": 2
		}
	}
}

```


## int isObject ( )

Returns a value indicating if the Json node has an *object* type.
### Return value

1 if the Json has an *object* type; otherwise, 0.
## Json getParent ( )

Returns the parent node of the current Json node.
### Return value

Parent Json node.
## void setString ( variable var )

Sets a string value and type to the current Json node. The function automatically casts number values to string type.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *string* value - string value.
  - *int* number - integer value.
  - *double* number - double value.
  - *float* number - float value.

## int isString ( )

Returns a value indicating if the Json node has a string type.
### Return value

1 if the Json has a string type; otherwise, 0.
## void clear ( )

Clears all data of the current Json node including type, value, name and all children. If the current Json node has a parent, it also removed from the parent Json node.
## removeChild ( variable var )

Removes the child Json node.
### Arguments

- *variable* **var** - Argument of one of the following types:

  - *Json* json - Json node.
  - *string* name - Name of the Json node.

### Return value

Removed child Json node.
## void clearChildren ( )

Clears all children of the current Json node.
## void copy ( Json source )

Copies type, name and value from the source Json node to the current Json node and adds the source Json child nodes as child nodes to the current Json node.
### Arguments

- *[Json](../../../api/library/common/class.json_usc.md)* **source** - Source Json node.

## Json find ( string name )

Finds Json node by its name in current Json node tree.
### Arguments

- *string* **name** - Name of the Json node.

### Return value

Founded Json node.
## int load ( string path )

Loads the data to the current Json node from the file with a given path.
### Arguments

- *string* **path** - Path of the file.

### Return value

1 if the Json node was loaded successfully; otherwise, 0.
## int parse ( string source )

Parses a given string into the Json node.


**Usage Example**


```cpp
Json json = new Json();
json.addChild("child_0", 1);

Json json_2 = new Json();
json_2.parse(json.getSubTree());

```


Now the json_2 node contains:


```text
{
	"child_0": 1
}

```


### Arguments

- *string* **source** - String to parse.

### Return value

1 if the string was parsed successfully; otherwise, 0.
## int save ( string path )

Saves the Json node into a file with a given path. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *string* **path** - Path to the file.

### Return value

1 if the file was saved successfully; otherwise, 0.
## string getTypeName ( )

Returns the name of the [type](#node_type) of the Json node.
### Return value

Name of the Json node type.
## void setInt ( int value )

Sets the specified integer value to the current Json node.
### Arguments

- *int* **value** - Value to be set to the current Json node.

## void setInt ( string name , int value )

Sets the specified integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *int* **value** - Value to be set to the target Json node.

## int getInt ( )

Returns the value of the current Json node as an integer value, if possible.
### Return value

Node value.
## int getInt ( string name )

Returns the value of the target Json node with the specified name as an integer value, if possible.
### Arguments

- *string* **name** - Name of the target Json node.

## void setVec2 ( const vec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const vec2 &* **value** - Vector setting the first two elements of the array-type Json node.

## vec2 getVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setVec3 ( const vec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const vec3 &* **value** - Vector setting the first three elements of the array-type Json node.

## vec3 getVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setVec4 ( const vec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const vec4 &* **value** - Vector setting the first four elements of the array-type Json node.

## vec4 getVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void setDVec2 ( const dvec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const dvec2 &* **value** - Vector setting the first two elements of the array-type Json node.

## dvec2 getDVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0, 0.0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setDVec3 ( const dvec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const dvec3 &* **value** - Vector setting the first three elements of the array-type Json node.

## dvec3 getDVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setDVec4 ( const dvec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const dvec4 &* **value** - Vector setting the first four elements of the array-type Json node.

## dvec4 getDVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void setIVec2 ( const ivec2 & value )

Sets the first two elements of the array-type Json node.
### Arguments

- *const ivec2 &* **value** - Vector setting the first two elements of the array-type Json node.

## ivec2 getIVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array a zero-vector (0, 0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void setIVec3 ( const ivec3 & value )

Sets the first three elements of the array-type Json node.
### Arguments

- *const ivec3 &* **value** - Vector setting the first three elements of the array-type Json node.

## ivec3 getIVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void setIVec4 ( const ivec4 & value )

Sets the first four elements of the array-type Json node.
### Arguments

- *const ivec4 &* **value** - Vector setting the first four elements of the array-type Json node.

## ivec4 getIVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0, 0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
