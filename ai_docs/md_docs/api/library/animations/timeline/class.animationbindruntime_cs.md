# Unigine::AnimationBindRuntime Class (CS)

**Inherits from:** AnimationBind


This class is used to manage runtime [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated. Runtime objects (such as widgets, windows, etc.) cannot be saved, they are created and assigned to bindings at run-time.


## AnimationBindRuntime Class

### Properties

## Widget Widget

The animated widget.
### Members

---

## AnimationBindRuntime ( )

Constructor. Creates an empty runtime object binding.
