# Unigine::NodeExtern Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


NodeExtern is a custom user-defined node created via API. The NodeExtern class is a wrapper for implementation of a custom node class inherited from the [NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cpp.md) class.


A NodeExtern node is created when the engine loads an instance of the custom node class. It can also be created directly by using the class constructor with a custom node class ID as an argument. In both cases, the NodeExtern node wraps the custom node class inherited from the NodeExternBase.


A custom user-defined node is created as follows:

> **Notice:** The custom user-defined node can be implemented on the C++ side only. So you should implement the custom node class in C++ and then use it on the C++ or UnigineScript side.


1. Inherit a custom node class from NodeExternBase: ```cpp #include <UnigineNodes.h> using namespace Unigine; // inherit a custom class from NodeExternBase class MyNode : public NodeExternBase { }; ```
2. Implement logic of the custom node and register the class via *[NodeExternBase::addClassID()](../../../api/library/nodes/class.nodeexternbase_cpp.md)*: > **Notice:** The custom node class isn't a node, as the NodeExternBase class isn't inherited from the [Node](../../../api/library/nodes/class.node_cpp.md) class. ```cpp #include <UnigineNodes.h> #include <UnigineEngine.h> #include "AppSystemLogic.h" #include "AppWorldLogic.h" using namespace Unigine; // inherit a custom class from NodeExternBase class MyNode : public NodeExternBase { public: // constructors MyNode(){} MyNode(void *node) : NodeExternBase(node){} // destructor virtual ~MyNode(){} // unique class ID virtual int getClassID() {return 1;} // set world transformation of the node void setWorldTransform(const Math::Mat4 &transform) {getNode()->setWorldTransform(transform);} // other methods // ... }; int main(int argc,char *argv[]) { // register the MyNode class NodeExternBase::addClassID<MyNode>(1); Unigine::EnginePtr engine(argc,argv); AppSystemLogic system_logic; AppWorldLogic world_logic; engine->main(&system_logic,&world_logic); return 0; } ``` If required, the custom node class can be [exported to UnigineScript](../../../api/library/nodes/class.nodeexternbase_cpp.md#export_class).
3. Create a custom node in one of the following ways: ```cpp // create a MyNode pointer directly: a NodeExtern node will be created as well MyNode *my_node_0 = new MyNode(); // obtain the NodeExtern node my_node_0->getNodeExtern(); // create a NodeExtern instance by MyNode's class ID NodeExternPtr my_node_1 = NodeExtern::create(1); // obtain the MyNode pointer if required MyNode *my_node_2 = (MyNode*)my_node_1->getNodeExtern(); ``` If the class has been [exported to UnigineScript](../../../api/library/nodes/class.nodeexternbase_cpp.md#export_class), you can perform the same on the UnigineScript side: ```cpp // create a MyNode pointer directly: a NodeExtern node will be created as well MyNode my_node_0 = new MyNode(); // obtain the NodeExtern node my_node_0.getNodeExtern(); // create a NodeExtern instance by MyNode's class ID NodeExtern my_node_1 = new NodeExtern(1); // obtain MyNode if required MyNode my_node_2 = class_cast("MyNode", node.getNodeExtern()); ```


### See Also


- The [NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cpp.md) class for the complete usage example of the NodeExtern and NodeExternBase classes.
- C++ sample


## NodeExtern Class

---

## static NodeExternPtr create ( int class_id )

Constructor. Creates a custom user-defined node. An instance of the custom node class will be created as well.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( )

Returns the [class ID](../../../api/library/nodes/class.nodeexternbase_cpp.md#addClassID_int_void) of the node.
### Return value

Class ID if the node exists; otherwise, 0.
## NodeExternBase * getNodeExtern ( )

Returns the pointer to the custom node class.
```cpp
// create a NodeExtern instance by MyNode's class ID
NodeExternPtr my_node_1 = NodeExtern::create(1);
// get the MyNode pointer
MyNode *my_node_2 = (MyNode*)my_node_1->getNodeExtern();

```


### Return value

Pointer to the custom node class.
## static int type ( )

Returns the type of the node.
### Return value

[NodeExtern](../../../api/library/nodes/class.node_cpp.md#NODE_EXTERN) type identifier.
