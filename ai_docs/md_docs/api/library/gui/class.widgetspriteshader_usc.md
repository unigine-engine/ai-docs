# Unigine::WidgetSpriteShader Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetSprite


This class creates a sprite to display a image with a custom post-process material applied.


### See Also


- UnigineScript sample


## WidgetSpriteShader Class

### Members

## void setMaterial ( Material material )

Sets a new post-process material for the widget.
### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - The post-process material.

## Material getMaterial () const

Returns the current post-process material for the widget.
### Return value

Current post-process material.
---

## static WidgetSpriteShader ( Gui gui , string name = 0 )

Constructor. Creates a new sprite with the specified texture and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the sprite will belong.
- *string* **name** - Path to the texture. This is an optional parameter.

## static WidgetSpriteShader ( string name = 0 )

Constructor. Creates a new sprite with the specified texture and adds it to the Engine GUI.
### Arguments

- *string* **name** - Path to the texture. This is an optional parameter.
