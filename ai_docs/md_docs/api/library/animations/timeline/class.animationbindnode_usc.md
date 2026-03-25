# Unigine::AnimationBindNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationBind


This class is used to manage node [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


## AnimationBindNode Class

### Members

## void setNode ( Node node )

Sets a new animated node.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - The animated node.

## Node getNode () const

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
## void setNodeDescription ( int id , string name )

Sets the description components of the animated node.
### Arguments

- *int* **id** - ID of the node, to be animated.
- *string* **name** - name of the node, to be animated.
