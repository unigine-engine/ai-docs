# Unigine Script Basic Utilities (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


To use functions listed on this page include the `unigine.h` script into your project (it can be found in the `data/core` directory). All the functions of this script are safe.


The `unigine.h` script also defines math constants, color codes and data types (for single or double precision coordinates).


## void swap ( variable v0 , variable v1 )

Interchanges values of two variables.
### Arguments

- *variable* **v0** - The first variable.
- *variable* **v1** - The second variable.


## void sleep ( float time )

Causes the currently executing [thread](../../../../code/uniginescript/language/control_statements/other_statements/thread.md) to sleep (cease execution) for the specified number of seconds. The sleep() function is thread-safe: when you set to sleep multiple threads, there are no side effects such as thread interferences appears.
### Arguments

- *float* **time** - Time of thread sleeping in seconds.


## Node node_cast ( Node node )

Converts a base node to its derived type.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be type-cast.

### Return value

Type-cast node.
## Node node_clone ( Node node )

Clones a node and its children and then converts the node to its derived type. It is used for correct cloning of nodes that have assigned bodies and joints.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be cloned.

### Return value

Type-cast copy of the node.
## Node node_append ( Node node )

Establishes [script ownership](../../../../code/uniginescript/memory_management.md#scripts) over the node and its children. It also casts nodes to their types. Do not forget, a node can have only one owner.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be appended.

### Return value

Appended node.
## Node node_remove ( Node node )

Releases [script ownership](../../../../code/uniginescript/memory_management.md#scripts) over the node and its children. It also casts nodes to their types. Do not forget, that an orphan node need to be assigned to another owner.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be released.

### Return value

Released node.
## void node_delete ( Node node )

Deletes a node and its children.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be deleted.


## Node node_load ( string name )

Loads a node from a file and establishes [script ownership](../../../../code/uniginescript/memory_management.md#scripts) over it and its children. It also casts nodes to their types. If a node cannot be found, it will lead to the crash.
### Arguments

- *string* **name** - Node file to be loaded.

### Return value

Loaded node.
## int node_save ( string name , Node node )

Saves a node into a `.node` file.
### Arguments

- *string* **name** - File to save the node into.
- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be saved.

### Return value

**1**, if the node is saved successfully; otherwise, **0**.
## Node node_editor ( string name )

Gets an Engine Editor node by the name and casts it to its type.
### Arguments

- *string* **name** - Node name.

### Return value

Type-cast node.
## Body body_cast ( Body body )

Converts a base body to its derived type.
### Arguments

- *[Body](../../../../api/library/physics/class.body_usc.md)* **body** - Body to be type-cast.

### Return value

Type-cast body.
## Body body_clone ( Body body , Object object = NULL )

Clones the body and then converts it to its derived type. It also assigns a copy to a given object if necessary. This function correctly clones joints of the body.
### Arguments

- *[Body](../../../../api/library/physics/class.body_usc.md)* **body** - Body to be cloned.
- *[Object](../../../../api/library/objects/class.object_usc.md)* **object** - Object, to which the copied body will be assigned. This is an optional argument.

### Return value

Type-cast copy of the body.
## Shape shape_cast ( Shape shape )

Converts a base shape to its derived type.
### Arguments

- *[Shape](../../../../api/library/physics/class.shape_usc.md)* **shape** - Shape to be type-cast.

### Return value

Type-cast shape.
## Shape shape_clone ( Shape shape )

Clones the shape and then converts it to its derived type. This function correctly clones joints of the shape.
### Arguments

- *[Shape](../../../../api/library/physics/class.shape_usc.md)* **shape** - Shape to be cloned.

### Return value

Type-cast copy of the shape.
## Joint joint_cast ( Joint joint )

Converts a base joint to its derived type.
### Arguments

- *[Joint](../../../../api/library/physics/class.joint_usc.md)* **joint** - Joint to be type-cast.

### Return value

Type-cast joint.
## Joint joint_clone ( Joint joint )

Clones the joint and then converts it to its derived type. This function correctly clones the joints.
### Arguments

- *[Joint](../../../../api/library/physics/class.joint_usc.md)* **joint** - Joint to be cloned.

### Return value

Type-cast copy of the joint.
## Widget widget_cast ( Widget widget )

Converts a base widget to its derived type.
### Arguments

- *[Widget](../../../../api/library/gui/class.widget_usc.md)* **widget** - Widget to be type-cast.

### Return value

Type-cast widget.
## void body_traversal ( Body body , string name )

Calls a specified function for a given body and its children.
### Arguments

- *[Body](../../../../api/library/physics/class.body_usc.md)* **body** - Body to be passed to a function.
- *string* **name** - Function to be called.


## void body_shape_traversal ( Body body , string name )

Calls a specified function for shapes of a given body and body's children.
### Arguments

- *[Body](../../../../api/library/physics/class.body_usc.md)* **body** - Body, the shapes of which will be passed to a function.
- *string* **name** - Function to be called.


## void body_joint_traversal ( Body body , string name )

Calls a specified function for joints of a given body and body's children.
### Arguments

- *[Body](../../../../api/library/physics/class.body_usc.md)* **body** - Body, the joints of which will be passed to a function.
- *string* **name** - Function to be called.


## void node_traversal ( Node node , string name )

Calls a specified function for a given node and its children.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be passed to a function.
- *string* **name** - Function to be called.


## void node_body_traversal ( Node node , string name )

Calls a specified function for bodies of a given node and its children.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node, the body of which will be passed to a function.
- *string* **name** - Function to be called.


## void node_shape_traversal ( Node node , string name )

Calls a specified function for shapes of a given node and its children.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node, the shapes of which will be passed to a function.
- *string* **name** - Function to be called.


## void node_joint_traversal ( Node node , string name )

Calls a specified function for joints of a given node and its children.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node, the joints of which will be passed to a function.
- *string* **name** - Function to be called.
