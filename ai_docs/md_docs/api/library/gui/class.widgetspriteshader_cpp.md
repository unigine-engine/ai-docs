# Unigine::WidgetSpriteShader Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetSprite


This class creates a sprite to display a image with a custom post-process material applied.


### See Also


- UnigineScript sample


## WidgetSpriteShader Class

### Members

## void setMaterial ( const const Ptr < Material > && material )

Sets a new post-process material for the widget.
### Arguments

- *const const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &&* **material** - The post-process material.

## const Ptr < Material > & getMaterial () const

Returns the current post-process material for the widget.
### Return value

Current post-process material.
---

## static WidgetSpriteShaderPtr create ( const Ptr < Gui > & gui , const char * name = 0 )

Constructor. Creates a new sprite with the specified texture and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the sprite will belong.
- *const char ** **name** - Path to the texture. This is an optional parameter.

## static WidgetSpriteShaderPtr create ( const char * name = 0 )

Constructor. Creates a new sprite with the specified texture and adds it to the Engine GUI.
### Arguments

- *const char ** **name** - Path to the texture. This is an optional parameter.
