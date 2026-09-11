# Unigine::Json Class (CS)


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


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		Json json = new Json();

		json.AddChild("child_0", 0);    // int
		json.AddChild("child_1", 1.1);   // float
		json.AddChild("child_2", "two");  // string

		// array
		Json array_0 = json.AddChild("array_0");
		array_0.SetArray();
		array_0.AddChild(null, 1);
		array_0.AddChild(null, 1);
		array_0.AddChild(null, 0);

		// object
		Json object_0 = json.AddChild("object_0");
		object_0.SetObject();
		object_0.AddChild("one", 5);
		object_0.AddChild("two", 6);
		object_0.AddChild("three", 7);

		// save the Json node to the file
		json.Save("json/my.json");

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


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		Json json = new Json();

		// load the Json node from my.json
		json.Load("json/my_array.json");

		// add the array node as a child
		Json array_1 = json.AddChild("array_1");
		array_1.SetArray();
		// add object nodes to the array
		for (int i = 0; i < 5; i++)
		{
			Json object_1 = array_1.AddChild();
			object_1.AddChild("name", String.Format("value_{0}", i));
			object_1.AddChild("value", i + 1);
		}

		// save the updated Json node to a new file
		json.Save("json/my_array.json");

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


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		Json json = new Json();

		// create an object node
		Json object_0 = json.AddChild("array_or_object?");
		object_0.SetObject();
		object_0.AddChild("name1", 1);
		object_0.AddChild("name2", 2);
		object_0.AddChild("name3", 3);
		// save to a file
		json.Save("json/object.json");
		// change the type to "array"
		object_0.SetArray();
		// save to another file
		json.Save("json/array.json");

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


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		float coefficient;
		String name;
		vec4 color;

		Json json = new Json();

		// load the Json node from the file
		json.Load("json/cubes.json");
		// get its child node
		Json cubes = json.GetChild("cubes");

		for (int i = 0; i < cubes.GetNumChildren(); i++)
		{
			// get a child node of the "cubes" node
			Json child = cubes.GetChild(i);

			// read the node name
			name = child.Read("name");
			// read the coefficient to a variable
			child.Read("coefficient", out coefficient);
			// read the color to a variable
			child.Read("color", out color);

			// create a dynamic mesh using the read values
			ObjectMeshDynamic box = Primitives.CreateBox(vec3.ONE * coefficient);
			box.Name = name;
			box.WorldPosition = new vec3(0.0f, 0.0f, 1.0f * coefficient);
			box.SetMaterialParameterFloat4("albedo_color", color, 0);
			Log.Message("The {0} box: {0}\n", child.GetName(), box.Name);

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


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		// get the "array_0" child
		Json a = json.GetChild("array_0");
		// get its value
		vec3 v = a.GetVec3();
		// print the result to the console
		Log.Message("{0} {1} {2}\n", v.x, v.y, v.z);

	}


```


By using the *write()* methods of the class, you can also add a new child nodes and edit values of the existing ones. For example:


```csharp
public partial class JsonClass : Component
{
	private void Init()
	{

		json.Load("json/cubes.json");

		// add a new child node of the object type
		Json cube = json.GetChild("cubes").AddChild("sixth");
		cube.SetObject();
		// write new child nodes with the specified values
		cube.Write("name", "cube_black");
		cube.Write("coefficient", 6.0);
		cube.Write("color", new vec4(0, 0, 0, 0));

		// write new values for the existing Json node
		cube = json.GetChild("cubes").GetChild("first");
		cube.Write("name", "cube_black");
		cube.Write("coefficient", 3.0);
		cube.Write("color", new vec4(0, 0, 0, 0));

		// save changes to the .json file
		json.Save("json/cubes.json");

	}


```


## Json Class

### Members

---

## Json ( )

Default constructor that creates an empty instance.
## Json ( string name )

Constructor that creates a JSON node with a given name.
### Arguments

- *string* **name** - Name of the Json node.

## void SetArray ( )


Sets the array type to the current Json node.


> **Notice:** This method can be called for a newly added node or for the existing node to change its type. However, in certain cases, this can lead to data loss. For example, if you change the type from *object* to *array*, names of the child nodes will be lost.


## int IsArray ( )

Returns a value indicating if the Json node has an array type.
### Return value

1 if the Json has an array type; otherwise, 0.
## void SetBool ( int arg1 )

Sets a boolean value and type to the current Json node.
### Arguments

- *int* **arg1** - Integer value.

## int GetBool ( )

Reads a boolean value of the current Json node.
### Return value

1 if the Json node has a bool type; otherwise, 0.
## int IsBool ( )

Returns a value indicating if the Json node has a bool type.
### Return value

1 if the Json has a bool type; otherwise, 0.
## Json GetChild ( int num )

### Arguments

- *int* **num** - Number of the child of the Json node.

### Return value

Child Json node.
## Json GetChild ( string name )

### Arguments

- *string* **name** - Name of the Json node.

### Return value

Child Json node.
## int IsChild ( string name )

Checks if a child node with a given name exists.
### Arguments

- *string* **name** - Name of the child node.

### Return value

1 if a child with the provided name exists; otherwise, 0.
## Json AddChild ( string name , double value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *string* **name** - Node name.
- *double* **value** - Node value.

### Return value

Child Json node.
## Json AddChild ( string name , int value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *string* **name** - Node name.
- *int* **value** - Node value.

### Return value

Child Json node.
## Json AddChild ( string name , string value )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *string* **name** - Node name.
- *string* **value** - Node value.

### Return value

Child Json node.
## Json AddChild ( string name )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *string* **name** - Node name.

### Return value

Child Json node.
## Json AddChild ( Json json )

Adds a new name-value pair as a child node to the current Json node.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - Node name.

### Return value

Child Json node.
## Json AddChild ( )

Adds a child node to the current Json node.
### Return value

Child Json node.
## string GetSubTree ( string name = 0 )

Returns a subtree of a Json node as the non-formatted string.
### Arguments

- *string* **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Non-formatted subtree.
## string GetFormattedSubTree ( string name = 0 )

Returns a subtree of a Json node as the formatted string.
### Arguments

- *string* **name** - The name of a child node. If there is a name, the function returns formatted subtree for this child Json node.

### Return value

Formatted subtree.
## void SetName ( string name )

Sets the given name to the Json node.
### Arguments

- *string* **name** - Name of the Json node.

## string GetName ( )

Returns the name of the current Json node.
### Return value

The name of the Json node.
## void SetNull ( )

Sets null type to the current Json node.
## int IsNull ( )

Returns a value indicating if the Json node has a null type.
### Return value

1 if the Json has a null type; otherwise, 0.
## void SetNumber ( double arg1 )

Sets a number value and type to the current Json node.
### Arguments

- *double* **arg1** - Double value.

## double GetNumber ( )

Returns the number value of the current Json node.
### Return value

Number value of the current Json node.
## int IsNumber ( )

Returns a value indicating if the Json node has a number type.
### Return value

1 if the Json has a number type; otherwise, 0.
## int GetNumChildren ( )

Returns the number of child nodes of the current Json node.
### Return value

Number of child nodes.
## void ReserveChildren ( int num )

Sets the reserved capacity of the Json node to store the specified number of child nodes.
### Arguments

- *int* **num** - Number of child nodes.

## void SetObject ( )

Sets object type to the current Json node.
## int IsObject ( )

Returns a value indicating if the Json node has an *object* type.
### Return value

1 if the Json has an *object* type; otherwise, 0.
## Json GetParent ( )

Returns the parent node of the current Json node.
### Return value

Parent Json node.
## void SetString ( string arg1 )

Sets a string value and type to the current Json node. The function automatically casts number values to string type.
### Arguments

- *string* **arg1** - String value.

## string GetString ( )

Returns the string value stored in this JSON node. Valid only when the node actually holds a string (**[IsString()](../../...md#isString_int)** returns true).
### Return value

String value of the current Json node.
## int IsString ( )

Returns a value indicating if the Json node has a string type.
### Return value

1 if the Json has a string type; otherwise, 0.
## void Clear ( )

Clears all data of the current Json node including type, value, name and all children. If the current Json node has a parent, it also removed from the parent Json node.
## Json RemoveChild ( Json json )

Removes the child Json node.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - Json node to be removed.

### Return value

Removed child Json node.
## Json RemoveChild ( string name )

Removes the child Json node.
### Arguments

- *string* **name** - Name of the Json node to be removed.

### Return value

Removed child Json node.
## void ClearChildren ( )

Clears all children of the current Json node.
## void Copy ( Json source )

Copies type, name and value from the source Json node to the current Json node and adds the source Json child nodes as child nodes to the current Json node.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **source** - Source Json node.

## Json Find ( string name )

Finds Json node by its name in current Json node tree.
### Arguments

- *string* **name** - Name of the Json node.

### Return value

Founded Json node.
## int Load ( string path )

Loads the data to the current Json node from the file with a given path.
### Arguments

- *string* **path** - Path of the file.

### Return value

1 if the Json node was loaded successfully; otherwise, 0.
## int Parse ( string source )

Parses a given string into the Json node.


**Usage Example**


```csharp
Json json = new Json();
json.AddChild("child_0", 1);

Json json_2 = new Json();
json_2.Parse(json.GetSubTree());

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
## int Save ( string path )

Saves the Json node into a file with a given path. Creates the given file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *string* **path** - Path to the file.

### Return value

1 if the file was saved successfully; otherwise, 0.
## void Read ( string name , out bool value )

Reads a boolean value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out bool* **value** - Target boolean variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out int value )

Reads an integer value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out int* **value** - Target integer variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out uint value )

Reads an unsigned integer value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out uint* **value** - Target unsigned integer variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out byte value )

Reads a character value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out byte* **value** - Target character variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out double value )

Reads a double value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out double* **value** - Target double variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out float value )

Reads a float value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out float* **value** - Target float variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out UGUID value )

Reads a value of a Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out [UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **value** - UGUID of the variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out vec2 value )

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out vec2* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out vec3 value )

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out vec3* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out vec4 value )

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out vec4* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out dvec2 value )

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out dvec2* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out dvec3 value )

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out dvec3* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out dvec4 value )

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out dvec4* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out ivec2 value )

Reads a two-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out ivec2* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out ivec3 value )

Reads a three-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out ivec3* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , out ivec4 value )

Reads a four-component value of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *out ivec4* **value** - Target vector variable to which the value of the Json node with the specified name is saved.

## void Read ( string name , int[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *int[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , byte[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *byte[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , double[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *double[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , float[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *float[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , string[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *string[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , vec2[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *vec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , vec3[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *vec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , vec4[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *vec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , dvec2[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *dvec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , dvec3[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *dvec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , dvec4[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *dvec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , ivec2[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *ivec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , ivec3[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *ivec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string name , ivec4[] OUT_value )

Reads values of the array-type Json node with the specified name to the specified target variable.
### Arguments

- *string* **name** - Name of the Json node.
- *ivec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( out bool value )

Reads a boolean value of the Json node to the specified target variable.
### Arguments

- *out bool* **value** - Target boolean variable to which the value of the Json node is saved.

## void Read ( out int value )

Reads an integer value of the Json node to the specified target variable.
### Arguments

- *out int* **value** - Target integer variable to which the value of the Json node is saved.

## void Read ( out byte value )

Reads a character value of the Json node to the specified target variable.
### Arguments

- *out byte* **value** - Target character variable to which the value of the Json node is saved.

## void Read ( out double value )

Reads a double value of the Json node to the specified target variable.
### Arguments

- *out double* **value** - Target double variable to which the value of the Json node is saved.

## void Read ( out float value )

Reads a float value of the Json node to the specified target variable.
### Arguments

- *out float* **value** - Target float variable to which the value of the Json node is saved.

## void Read ( out vec2 value )

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *out vec2* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void Read ( out vec3 value )

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *out vec3* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void Read ( out vec4 value )

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *out vec4* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void Read ( out dvec2 value )

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *out dvec2* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void Read ( out dvec3 value )

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *out dvec3* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void Read ( out dvec4 value )

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *out dvec4* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void Read ( out ivec2 value )

Reads a two-component value of the array-type Json node to the specified target variable.
### Arguments

- *out ivec2* **value** - Target vector variable to which two components of the array-type Json node are saved.

## void Read ( out ivec3 value )

Reads a three-component value of the array-type Json node to the specified target variable.
### Arguments

- *out ivec3* **value** - Target vector variable to which three components of the array-type Json node are saved.

## void Read ( out ivec4 value )

Reads a four-component value of the array-type Json node to the specified target variable.
### Arguments

- *out ivec4* **value** - Target vector variable to which four components of the array-type Json node are saved.

## void Read ( bool[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *bool[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( int[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *int[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( byte[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *byte[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( double[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *double[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( float[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *float[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( string[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *string[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( vec2[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *vec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( vec3[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *vec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( vec4[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *vec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( dvec2[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *dvec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( dvec3[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *dvec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( dvec4[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *dvec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( ivec2[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *ivec2[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( ivec3[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *ivec3[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Read ( ivec4[] OUT_value )

Reads values of the array-type Json node to the specified target variable.
### Arguments

- *ivec4[]* **OUT_value** - Array to which components of the array-type Json node are saved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## string Read ( string name )

Returns a value of a Json node with the specified name as a string.
### Arguments

- *string* **name** - Name of the Json node.

### Return value

Node value.
## void Write ( string name , bool value )

Writes the specified boolean value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *bool* **value** - Boolean value to be written to the Json node with the specified name.

## void Write ( string name , int value )

Writes the specified integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *int* **value** - Integer value to be written to the Json node with the specified name.

## void Write ( string name , uint value )

Writes the specified unsigned integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *uint* **value** - Unsigned integer value to be written to the Json node with the specified name.

## void Write ( string name , byte value )

Writes the specified character value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *byte* **value** - Character value to be written to the Json node with the specified name.

## void Write ( string name , string value )

Writes the specified value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *string* **value** - Value to be written to the Json node with the specified name.

## void Write ( string name , double value )

Writes the specified double value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *double* **value** - Double value to be written to the Json node with the specified name.

## void Write ( string name , float value )

Writes the specified float value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *float* **value** - Float value to be written to the Json node with the specified name.

## void Write ( string name , vec2 value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec2* **value** - Two-component value to be written to the Json node with the specified name.

## void Write ( string name , vec3 value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec3* **value** - Three-component value to be written to the Json node with the specified name.

## void Write ( string name , vec4 value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec4* **value** - Four-component value to be written to the Json node with the specified name.

## void Write ( string name , dvec2 value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec2* **value** - Two-component value to be written to the Json node with the specified name.

## void Write ( string name , dvec3 value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec3* **value** - Three-component value to be written to the Json node with the specified name.

## void Write ( string name , dvec4 value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec4* **value** - Four-component value to be written to the Json node with the specified name.

## void Write ( string name , ivec2 value )

Writes the specified two-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec2* **value** - Two-component value to be written to the Json node with the specified name.

## void Write ( string name , ivec3 value )

Writes the specified three-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec3* **value** - Three-component value to be written to the Json node with the specified name.

## void Write ( string name , ivec4 value )

Writes the specified four-component value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec4* **value** - Four-component value to be written to the Json node with the specified name.

## void Write ( string name , int[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *int[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , byte[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *byte[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , double[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *double[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , float[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *float[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , string[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *string[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , vec2[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec2[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , vec3[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec3[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , vec4[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *vec4[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , dvec2[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec2[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , dvec3[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec3[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , dvec4[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *dvec4[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , ivec2[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec2[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , ivec3[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec3[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , ivec4[] value )

Writes the specified values to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *ivec4[]* **value** - Array of values to be written to the Json node with the specified name.

## void Write ( string name , UGUID value )

Writes the specified value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **value** - UGUID of the value to be written to the Json node with the specified name.

## void Write ( UGUID value )

Writes the specified value to the current Json node.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **value** - UGUID of the value to be written to the Json node.

## void Write ( bool value )

Writes the specified boolean value to the current Json node.
### Arguments

- *bool* **value** - Boolean value to be written to the current Json node.

## void Write ( int value )

Writes the specified integer value to the current Json node.
### Arguments

- *int* **value** - Integer value to be written to the current Json node.

## void Write ( byte value )

Writes the specified character value to the current Json node.
### Arguments

- *byte* **value** - Character value to be written to the current Json node.

## void Write ( string value )

Writes the specified value to the current Json node.
### Arguments

- *string* **value** - Value to be written to the current Json node.

## void Write ( double value )

Writes the specified double value to the current Json node.
### Arguments

- *double* **value** - Double value to be written to the current Json node.

## void Write ( float value )

Writes the specified float value to the current Json node.
### Arguments

- *float* **value** - Float value to be written to the current Json node.

## void Write ( vec2 value )

Writes the specified two-component value to the current Json node.
### Arguments

- *vec2* **value** - Two-component value to be written to the current Json node.

## void Write ( vec3 value )

Writes the specified three-component value to the current Json node.
### Arguments

- *vec3* **value** - Three-component value to be written to the current Json node.

## void Write ( vec4 value )

Writes the specified four-component value to the current Json node.
### Arguments

- *vec4* **value** - Four-component value to be written to the current Json node.

## void Write ( dvec2 value )

Writes the specified two-component value to the current Json node.
### Arguments

- *dvec2* **value** - Two-component value to be written to the current Json node.

## void Write ( dvec3 value )

Writes the specified three-component value to the current Json node.
### Arguments

- *dvec3* **value** - Three-component value to be written to the current Json node.

## void Write ( dvec4 value )

Writes the specified four-component value to the current Json node.
### Arguments

- *dvec4* **value** - Four-component value to be written to the current Json node.

## void Write ( ivec2 value )

Writes the specified two-component value to the current Json node.
### Arguments

- *ivec2* **value** - Two-component value to be written to the current Json node.

## void Write ( ivec3 value )

Writes the specified three-component value to the current Json node.
### Arguments

- *ivec3* **value** - Three-component value to be written to the current Json node.

## void Write ( ivec4 value )

Writes the specified four-component value to the current Json node.
### Arguments

- *ivec4* **value** - Four-component value to be written to the current Json node.

## void Write ( bool[] value )

Writes the specified values to the current Json node.
### Arguments

- *bool[]* **value** - Array of values to be written to the current Json node.

## void Write ( int[] value )

Writes the specified values to the current Json node.
### Arguments

- *int[]* **value** - Array of values to be written to the current Json node.

## void Write ( byte[] value )

Writes the specified values to the current Json node.
### Arguments

- *byte[]* **value** - Array of values to be written to the current Json node.

## void Write ( double[] value )

Writes the specified values to the current Json node.
### Arguments

- *double[]* **value** - Array of values to be written to the current Json node.

## void Write ( float[] value )

Writes the specified values to the current Json node.
### Arguments

- *float[]* **value** - Array of values to be written to the current Json node.

## void Write ( string[] value )

Writes the specified values to the current Json node.
### Arguments

- *string[]* **value** - Array of values to be written to the current Json node.

## void Write ( vec2[] value )

Writes the specified values to the current Json node.
### Arguments

- *vec2[]* **value** - Array of values to be written to the current Json node.

## void Write ( vec3[] value )

Writes the specified values to the current Json node.
### Arguments

- *vec3[]* **value** - Array of values to be written to the current Json node.

## void Write ( vec4[] value )

Writes the specified values to the current Json node.
### Arguments

- *vec4[]* **value** - Array of values to be written to the current Json node.

## void Write ( dvec2[] value )

Writes the specified values to the current Json node.
### Arguments

- *dvec2[]* **value** - Array of values to be written to the current Json node.

## void Write ( dvec3[] value )

Writes the specified values to the current Json node.
### Arguments

- *dvec3[]* **value** - Array of values to be written to the current Json node.

## void Write ( dvec4[] value )

Writes the specified values to the current Json node.
### Arguments

- *dvec4[]* **value** - Array of values to be written to the current Json node.

## void Write ( ivec2[] value )

Writes the specified values to the current Json node.
### Arguments

- *ivec2[]* **value** - Array of values to be written to the current Json node.

## void Write ( ivec3[] value )

Writes the specified values to the current Json node.
### Arguments

- *ivec3[]* **value** - Array of values to be written to the current Json node.

## void Write ( ivec4[] value )

Writes the specified values to the current Json node.
### Arguments

- *ivec4[]* **value** - Array of values to be written to the current Json node.

## string GetTypeName ( )

Returns the name of the [type](#node_type) of the Json node.
### Return value

Name of the Json node type.
## void SetInt ( int value )

Sets the specified integer value to the current Json node.
### Arguments

- *int* **value** - Value to be set to the current Json node.

## void SetInt ( string name , int value )

Sets the specified integer value to the target Json node with the specified name. In case such node is not found, a new one is added with the name specified.
### Arguments

- *string* **name** - Name of the target Json node.
- *int* **value** - Value to be set to the target Json node.

## int GetInt ( )

Returns the value of the current Json node as an integer value, if possible.
### Return value

Node value.
## int GetInt ( string name )

Returns the value of the target Json node with the specified name as an integer value, if possible.
### Arguments

- *string* **name** - Name of the target Json node.

## void SetVec2 ( vec2 value )

Sets the first two elements of the array-type Json node.
### Arguments

- *vec2* **value** - Vector setting the first two elements of the array-type Json node.

## vec2 GetVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void SetVec3 ( vec3 value )

Sets the first three elements of the array-type Json node.
### Arguments

- *vec3* **value** - Vector setting the first three elements of the array-type Json node.

## vec3 GetVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void SetVec4 ( vec4 value )

Sets the first four elements of the array-type Json node.
### Arguments

- *vec4* **value** - Vector setting the first four elements of the array-type Json node.

## vec4 GetVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array, a zero-vector (0.0f, 0.0f, 0.0f, 0.0f) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void SetDVec2 ( dvec2 value )

Sets the first two elements of the array-type Json node.
### Arguments

- *dvec2* **value** - Vector setting the first two elements of the array-type Json node.

## dvec2 GetDVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array, a zero-vector (0.0, 0.0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void SetDVec3 ( dvec3 value )

Sets the first three elements of the array-type Json node.
### Arguments

- *dvec3* **value** - Vector setting the first three elements of the array-type Json node.

## dvec3 GetDVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void SetDVec4 ( dvec4 value )

Sets the first four elements of the array-type Json node.
### Arguments

- *dvec4* **value** - Vector setting the first four elements of the array-type Json node.

## dvec4 GetDVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0.0, 0.0, 0.0, 0.0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
## void SetIVec2 ( ivec2 value )

Sets the first two elements of the array-type Json node.
### Arguments

- *ivec2* **value** - Vector setting the first two elements of the array-type Json node.

## ivec2 GetIVec2 ( )

Returns a two-component vector composed of the first two elements of the array-type Json node. If the node is not an array a zero-vector (0, 0) shall be returned.
### Return value

Vector composed of the first two elements of the array-type Json node.
## void SetIVec3 ( ivec3 value )

Sets the first three elements of the array-type Json node.
### Arguments

- *ivec3* **value** - Vector setting the first three elements of the array-type Json node.

## ivec3 GetIVec3 ( )

Returns a three-component vector composed of the first three elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0) shall be returned.
### Return value

Vector composed of the first three elements of the array-type Json node.
## void SetIVec4 ( ivec4 value )

Sets the first four elements of the array-type Json node.
### Arguments

- *ivec4* **value** - Vector setting the first four elements of the array-type Json node.

## ivec4 GetIVec4 ( )

Returns a four-component vector composed of the first four elements of the array-type Json node. If the node is not an array a zero-vector (0, 0, 0, 0) shall be returned.
### Return value

Vector composed of the first four elements of the array-type Json node.
