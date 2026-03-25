# Unigine::NodeExtern Class (CS)

**Inherits from:** Node


NodeExtern is a custom user-defined node created via API. The NodeExtern class is a wrapper for implementation of a custom node class inherited from the [NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cs.md) class.


A NodeExtern node is created when the engine loads an instance of the custom node class. It can also be created directly by using the class constructor with a custom node class ID as an argument. In both cases, the NodeExtern node wraps the custom node class inherited from the NodeExternBase.


### See Also


- The [NodeExternBase](../../../api/library/nodes/class.nodeexternbase_cs.md) class for the complete usage example of the NodeExtern and NodeExternBase classes.
- C++ sample


## NodeExtern Class

### Members

---

## NodeExtern ( int class_id )

Constructor. Creates a custom user-defined node. An instance of the custom node class will be created as well.
### Arguments

- *int* **class_id** - Unique class ID.

## int GetClassID ( )

Returns the [class ID](../../../api/library/nodes/class.nodeexternbase_cs.md#addClassID_int_void) of the node.
### Return value

Class ID if the node exists; otherwise, 0.
## NodeExternBase GetNodeExtern ( )

Returns the pointer to the custom node class.
### Return value

Pointer to the custom node class.
## static int type ( )

Returns the type of the node.
### Return value

[NodeExtern](../../../api/library/nodes/class.node_cs.md#NODE_EXTERN) type identifier.
