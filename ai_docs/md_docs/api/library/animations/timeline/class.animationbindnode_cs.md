# Unigine::AnimationBindNode Class (CS)

**Inherits from:** AnimationBind


This class is used to manage node [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated.


## AnimationBindNode Class

### Properties

## Node Node

The animated node.
## 🔒︎ int NodeDescriptionID

The ID of the node, to be animated.
## 🔒︎ string NodeDescriptionName

The name of the node, to be animated.
### Members

---

## AnimationBindNode ( )

Constructor. Creates an empty node binding.
## void SetNodeDescription ( int id , string name )

Sets the description components of the animated node.
### Arguments

- *int* **id** - ID of the node, to be animated.
- *string* **name** - name of the node, to be animated.
