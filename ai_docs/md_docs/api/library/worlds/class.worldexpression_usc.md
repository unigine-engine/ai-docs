# Unigine.WorldExpression Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create a [world expression](../../../objects/worlds/world_expression/index.md), that executes an arbitrary expression (a script). An expression can be executed for the other nodes if they are assigned as child nodes of WorldExpression. The child nodes will inherit transformations (if any) of the world expression and will be transformed relative to the pivot point of WorldExpression.


#### Implementing World Expression Script


A WorldExpression script can be implemented as follows:


- As a simple sequence of functions' calls. For example: ```cpp // get the WorldExpression node Node node = getNode(); // apply transformation to the WorldExpression node node.setTransform(rotateX(cos(time * 3.0f) * 2.0f) * rotateY(sin(time * 2.0f) * 4.0f) * rotateZ(sin(time * 1.0f) * 8.0f) * translate(0.0f,0.0f,1.1f)); ```
- As a set of functions and classes. For example: ```cpp // create resources. This function is called on world load, when not all of the nodes can be loaded void __constructor__() { ... } // delete the created resources void __destructor__() { ... } /* */ // implement any required functions void print_message() { log.message("Hello from WorlExpression!\n"); } // implement a function that the WorldExpression will execute each frame void my_update() { ... print_message(); ... } // execute the update function my_update(); ``` > **Notice:** Do not forget to call the function that should be executed each frame in the script.


#### Inter-Script Communication


Each WorldExpression has its own scope. You cannot directly set or get variables to or from the WorldExpression (as memory corruption occurs).


- If a WorldExpression calls a function of a world script: ```cpp // World script namespace WorldScriptScope { void worldScriptFunc(string arg) { log.message("World script code: %s\n",arg); } } ``` ```cpp // WorldExpression engine.world.call("WorldScriptScope::worldScriptFunc","hello from WorldExpression"); ```
- If a world script calls a function of a WorldExpression: ```cpp // World script namespace WorldScriptScope { void worldScriptFunc(WorldExpression expression) { expression.call("worldExpressionFunc","hello from the world script"); } } ``` ```cpp // WorldExpression void worldExpressionFunc(string arg) { log.message("WorldExpression code: %s\n",arg); } ```


#### Script Functions


The following internal functions are available within the WorldExpression script:


- *Node getNode()* - returns the WorldExpression node.
- *Node getChild(int num)* - returns the WorldExpression child node by its number. If the child is not found, returns NULL.
- *int getNumChilds()* - returns the number of WorldExpression children.
- *Node getParent()* - returns the WorldExpression parent node. If there is no parent, returns NULL.


To get the WorldExpression node and its parent, you can write the following in the WorldExpression script:


```cpp
Node node = getNode();
Node parent = node.getParent();

```


Now you can, for example, operate with all of the WorldExpression children as follows:


```cpp
forloop(int i = 0; getNumChilds()) {
	Node child = getChild(i);
	log.message("The type of the node is: %s\n",child.getTypeName());
}
// this example shows the type of each WorldExpression child

```


### See Also


UnigineScript samples:


-
-
-
-
-
-


## WorldExpression Class

### Members

## int isCompiled () const

Returns the current value indicating if the given expression has been compiled. it is automatically called on world load or after *[setExpression()](#setExpression_cstr_int)* is used.
### Return value

Current the given expression has been compiled
## void setIFps ( float ifps )

Sets a new constant frame duration used to execute the expression. It can be used to decrease the frame rate to get higher performance. 0 means that the expression is executed at the same frame rate as the main application window.
### Arguments

- *float* **ifps** - The Frame duration (inverse FPS) in seconds (*1/FPS*). If a too small value is provided, 1E-6 will be used instead.

## float getIFps () const

Returns the current constant frame duration used to execute the expression. It can be used to decrease the frame rate to get higher performance. 0 means that the expression is executed at the same frame rate as the main application window.
### Return value

Current Frame duration (inverse FPS) in seconds (*1/FPS*). If a too small value is provided, 1E-6 will be used instead.
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated.
### Return value

Current distance from the camera within which the object should be updated.
---

## static WorldExpression ( )

Constructor. Creates an arbitrary expression to be executed.
## int setExpression ( string src )

Sets the arbitrary expression to be executed.


> **Notice:** The expression passed as an argument must be wrapped with curly braces {} as they define the world expression scope.


If the expression is stored in a file, this file should be included as follows:


```cpp
expression.setExpression("{\n#include <my_project/scripts/my_expression.h>\n}");
```


The path should be specified relative to the `data` directory.

### Arguments

- *string* **src** - An executable expression.

### Return value

**1** if the expression is set successfully; otherwise, **0**.
## string getExpression ( )

Returns the executable expression.
### Return value

The executable expression.
## int isFunction ( string name , int num_args )

Returns a value indicating if the given world expression has the function with specified name and number of arguments.
### Arguments

- *string* **name** - The name of the function.
- *int* **num_args** - The number of arguments.

### Return value

**1** if the expression exists; otherwise, **0**.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
## int setExpressionName ( string name )

Loads an expression from the given file.
### Arguments

- *string* **name** - Expression file name.

### Return value

**1** if the expression is successfully loaded from the given file; otherwise, **0**.
## string getExpressionName ( )

Returns the name of the expression file.
### Return value

Expression file name.
