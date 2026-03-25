# Unigine::AnimationBindRuntime Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationBind


This class is used to manage runtime [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects like widgets and windows) at the playback stage.


Bindings are used to store, search, and obtain real engine objects that are actually animated. Runtime objects (such as widgets, windows, etc.) cannot be saved, they are created and assigned to bindings at run-time.


## AnimationBindRuntime Class

### Members

## void setWidget ( Widget widget )

Sets a new animated widget.
### Arguments

- *[Widget](../../../../api/library/gui/class.widget_usc.md)* **widget** - The animated widget.

## Widget getWidget () const

Returns the current animated widget.
### Return value

Current animated widget.
---

## AnimationBindRuntime ( )

Constructor. Creates an empty runtime object binding.
