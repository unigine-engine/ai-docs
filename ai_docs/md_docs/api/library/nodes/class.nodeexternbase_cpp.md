# Unigine::NodeExternBase Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Base


The base class that is used to implement logic of [custom user-defined nodes](../../../api/library/nodes/class.nodeextern_cpp.md). The custom node class should be inherited from NodeExternBase.


> **Notice:** NodeExternBase isn't a node (it isn't inherited from the [Node](../../../api/library/nodes/class.node_cpp.md) class). So when the engine loads an instance of the custom node class, a [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md) node is created. It wraps implementation of the custom node class inherited from the NodeExternBase class.


### Usage Example


To implement logic of a custom node, do the following:

> **Notice:** The custom user-defined node can be implemented on the C++ side only. So the example below shows how to implement such node in C++ and then use in both C++ and UnigineScript.


1. Inherit your custom node class from *NodeExternBase*.
2. Implement constructors, destructor and all required methods.
3. Register the class via *addClassID()*.
4. (Optional) If required, export the class and its functions to UnigineScript.


`MyNode.h` contains implementation of the custom *MyNode* class inherited from the NodeExternBase class.


```cpp
#include <UnigineNodes.h>

using namespace Unigine;

// inherit a custom class from NodeExternBase
class MyNode : public NodeExternBase
{
public:

	// constructors
	MyNode();
	MyNode(void *node);
	// destructor
	virtual ~MyNode();

	// unique class ID
	virtual int getClassID();

	// save and restore the node state
	virtual int saveState(const StreamPtr &stream);
	virtual int restoreState(const StreamPtr &stream);

	// save and restore the node pointer
	static void savePointer(const StreamPtr &stream, MyNode *node);
	static NodeExternBase *restorePointer(const StreamPtr &stream);

	// set world transformation of the node
	void setWorldTransform(const Math::Mat4 &transform);
};

```


`MyNode.cpp` contains implementation of MyNode's methods.


```cpp
#include "MyNode.h"

// constructor with no arguments
MyNode::MyNode()
{
	Log::warning("MyNode::MyNode(): called\n");
}
// constructor with 1 argument
MyNode::MyNode(void *node)
	: NodeExternBase(node)
{
	Log::warning("MyNode::MyNode(void*): called\n");
}
// destructor
MyNode::~MyNode()
{
	Log::warning("MyNode::~MyNode(): called\n");
}
// returns the class ID of MyNode
int MyNode::getClassID()
{
	return 1;
}
// save the node state
int MyNode::saveState(const StreamPtr &stream)
{
	Log::warning("MyNode::saveState(): called\n");
	return NodeExternBase::saveState(stream);
}
// restore the node state
int MyNode::restoreState(const StreamPtr &stream)
{
	Log::warning("MyNode::restoreState(): called\n");
	return NodeExternBase::restoreState(stream);
}
// save the node pointer
void MyNode::savePointer(const StreamPtr &stream, MyNode *node)
{
	Log::warning("MyNode::savePointer(): called\n");
	return NodeExternBase::savePointer(stream, node);
}
// restore the node pointer
NodeExternBase *MyNode::restorePointer(const StreamPtr &stream)
{
	Log::warning("MyNode::restorePointer(): called\n");
	return NodeExternBase::restorePointer(stream);
}

// set world transformation of the node
void MyNode::setWorldTransform(const Math::Mat4 &transform)
{
	getNode()->setWorldTransform(transform);
	Log::message("MyNode::setWorldTransform(): called\n");
}

```


In `unigine_project.cpp` the MyNode class is registered.


```cpp
#include <UnigineEngine.h>
#include "AppSystemLogic.h"
#include "AppWorldLogic.h"
#include "MyNode.h"

int main(int argc,char *argv[]) {

	// register the MyNode class
	NodeExternBase::addClassID<MyNode>(1);

	Unigine::EnginePtr engine(argc,argv);

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	engine->main(&system_logic,&world_logic);

	return 0;
}

```


In `AppWorldLogic.cpp`, approaches to work with the MyNode class are shown: you can directly create an instance of the MyNode class, or you can create an instance of the NodeExtern class by using MyNode's class ID. In both cases, an instance of the MyNode class is created.


```cpp
#include "AppWorldLogic.h"
#include "MyNode.h"

int AppWorldLogic::init() {

	// create a MyNode pointer directly
	MyNode *my_node_0 = new MyNode();
	// call a member function
	my_node_0->setWorldTransform(Math::translate(Math::Vec3(0.5)));

	// create a NodeExtern instance by MyNode's class ID
	NodeExternPtr my_node_1 = NodeExtern::create(1);
	// obtain the MyNode pointer
	MyNode *my_node_2 = (MyNode*)my_node_1->getNodeExtern();
	// call the MyNode member function
	my_node_2->setWorldTransform(Math::translate(Math::Vec3(1.0)));

	return 1;
}

```


```text
MyNode::MyNode(): called
MyNode::setWorldTransform(): called
MyNode::MyNode(void*): called
MyNode::setWorldTransform(): called
MyNode::~MyNode(): called

```


#### Exporting to UnigineScript


To use the custom node on the UnigineScript side, export the class and its functions to UnigineScript.


`unigine_project.cpp`:


```cpp
#include <UnigineEngine.h>
#include <UnigineInterface.h>
#include "AppSystemLogic.h"
#include "AppWorldLogic.h"
#include "MyNode.h"

int main(int argc,char *argv[]) {

	// register the MyNode class
	NodeExternBase::addClassID<MyNode>(1);

	// export the MyNode class
	ExternClass<MyNode> *my_node = MakeExternClassSaveRestoreStatePointer<MyNode>();
	my_node->addConstructor();
	my_node->addFunction("grab", &MyNode::grab);
	my_node->addFunction("release", &MyNode::release);
	my_node->addFunction("getNode", &MyNode::getNode);
	my_node->addFunction("setWorldTransform", &MyNode::setWorldTransform);
	Interpreter::addExternClass("MyNode", my_node);

	Unigine::EnginePtr engine(argc,argv);

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	engine->main(&system_logic,&world_logic);

	return 0;
}

```


And then use the MyNode class on the UnigineScript side:


```cpp
#include <core/unigine.h>

int init() {

	// create MyNode
	MyNode my_node_0 = new MyNode();
	my_node_0.setWorldTransform(Mat4(translate(0.0f, 0.0f, 1.0f)));

	// create NodeExtern by class ID
	NodeExtern node = new NodeExtern(1);
	MyNode my_node_1 = class_cast("MyNode", node.getNodeExtern());
	my_node_1.setWorldTransform(Mat4(translate(0.0f, 0.0f, -1.0f)));

	return 1;
}

```


## NodeExternBase Class

---

## template < class Type >

## static addClassID ( int class_id )

Registers the custom node class with a unique class ID.
```cpp
// register the MyNode class
NodeExternBase::addClassID<MyNode>(1);

```


### Arguments

- *int* **class_id** - Unique class ID.

## void copy ( NodeExternBase * node , int is_root )

Copies the current custom node into the given one.
### Arguments

- *[NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cpp.md) ** **node** - Pointer to a target node.
- *int* **is_root** - Unique class ID.

## BoundBox getBoundBox ( )

Returns the bounding box of the custom node.
### Return value

The bounding box.
## BoundSphere getBoundSphere ( )

Returns the bounding sphere of the custom node.
### Return value

The bounding sphere.
## int getClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Ptr < Node > getNode ( )

Returns the Node smart pointer.
### Return value

Node smart pointer.
## Ptr < NodeExtern > getNodeExtern ( )

Returns the [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md) instance that is created on loading the custom node.
### Return value

NodeExtern smart pointer.
## int loadWorld ( const Ptr < Xml > & xml )

Loads a node state from the Xml.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.

### Return value

Returns 1 if the node state was successfully loaded; otherwise, 0 is returned.
## void renderHandler ( )

Renders the handler for the custom user-defined node.
## void renderVisualizer ( )

Renders the visualizer for the custom user-defined node.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## bool saveState ( const Ptr < Stream > & stream )

Saves a node state into the stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreState()](#restoreState_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
node->saveState(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
node->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )

Restores a node state from the stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [saveState()](#saveState_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
node->saveState(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
node->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## int saveWorld ( const Ptr < Xml > & xml )

Saves a node state into the Xml.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.

### Return value

1 if the node state was successfully saved; otherwise, 0 is returned.
## void swap ( NodeExternBase * node )

Swaps two custom nodes.
### Arguments

- *[NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cpp.md) ** **node** - Pointer to the custom node to swap.

## void updateEnabled ( )

Updates enabled.
## void updateTransform ( )

Updates transformation matrix of the custom node.
