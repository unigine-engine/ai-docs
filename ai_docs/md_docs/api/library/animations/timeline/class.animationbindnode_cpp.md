# Unigine::AnimationBindNode Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This class is used to manage node [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


## AnimationBindNode Class

### Members

## void setNode ( const Ptr < Node >& node )

Sets a new animated node.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>&* **node** - The animated node.

## Ptr < Node > getNode () const

Returns the current animated node.
### Return value

Current animated node.
## getNodeDescriptionID () const

Returns the current ID of the node, to be animated.
### Return value

Current ID of the node.
## const char * getNodeDescriptionName () const

Returns the current name of the node, to be animated.
### Return value

Current name of the node.
---

## AnimationBindNode ( )

Constructor. Creates an empty node binding.
## void setNodeDescription ( int id , const char * name )

Sets the description components of the animated node.
### Arguments

- *int* **id** - ID of the node, to be animated.
- *const char ** **name** - name of the node, to be animated.
