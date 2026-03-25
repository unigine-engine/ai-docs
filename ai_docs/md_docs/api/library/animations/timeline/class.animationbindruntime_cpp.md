# Unigine::AnimationBindRuntime Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This class is used to manage runtime [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated. Runtime objects (such as widgets, windows, etc.) cannot be saved, they are created and assigned to bindings at run-time.


## AnimationBindRuntime Class

### Members

## void setWidget ( const Ptr < Widget >& widget )

Sets a new animated widget.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../../api/library/gui/class.widget_cpp.md)>&* **widget** - The animated widget.

## Ptr < Widget > getWidget () const

Returns the current animated widget.
### Return value

Current animated widget.
---

## AnimationBindRuntime ( )

Constructor. Creates an empty runtime object binding.
