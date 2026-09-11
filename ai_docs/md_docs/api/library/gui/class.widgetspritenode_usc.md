# Unigine::WidgetSpriteNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetSprite


This class is used to display separate nodes together with all their children. This widget supports alpha channel masking. But unlike [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md), it does not support engine postprocesses (like HDR, DOF, motion blur, glow, etc.); only [postprocess materials](../../../content/materials/library/postprocess/index.md) can be applied to it.


## WidgetSpriteNode Class

### Members

## void setNode ( Node node )

Sets a new node set for displaying.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - The node set for displaying

## Node getNode () const

Returns the current node set for displaying.
### Return value

Current node set for displaying
## void setIFps ( float ifps )

Sets a new frame duration used to render the sprite node viewport, in seconds (*1/FPS*). For example, it can be used to decrease the frame rate to get higher performance. If a too small value is provided, **1E-6** will be used instead.
### Arguments

- *float* **ifps** - The frame duration used to render the sprite node viewport

## float getIFps () const

Returns the current frame duration used to render the sprite node viewport, in seconds (*1/FPS*). For example, it can be used to decrease the frame rate to get higher performance. If a too small value is provided, **1E-6** will be used instead.
### Return value

Current frame duration used to render the sprite node viewport
## void setLightUsage ( int usage )

Sets a new type of lighting for the sprite node. One of the following values:
- [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_WORLD_LIGHT)
- [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_AUX_LIGHT)
- [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_NODE_LIGHT)

### Arguments

- *int* **usage** - The type of lighting for the sprite node

## int getLightUsage () const

Returns the current type of lighting for the sprite node. One of the following values:
- [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_WORLD_LIGHT)
- [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_AUX_LIGHT)
- [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_NODE_LIGHT)

### Return value

Current type of lighting for the sprite node
## void setSkipFlags ( int flags )

Sets a new [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) set for the current viewport. Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB

### Arguments

- *int* **flags** - The skip flags set for the current viewport

## int getSkipFlags () const

Returns the current [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) set for the current viewport. Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB

### Return value

Current skip flags set for the current viewport
## void setEnvironmentTexturePath ( string path )

Sets a new path to the environment texture.
### Arguments

- *string* **path** - The path to the environment texture

## const char * getEnvironmentTexturePath () const

Returns the current path to the environment texture.
### Return value

Current path to the environment texture
## void setModelview ( Mat4 modelview )

Sets a new model-view matrix.
### Arguments

- *Mat4* **modelview** - The model-view matrix

## Mat4 getModelview () const

Returns the current model-view matrix.
### Return value

Current model-view matrix
## void setProjection ( mat4 projection )

Sets a new projection matrix.
### Arguments

- *mat4* **projection** - The projection matrix

## mat4 getProjection () const

Returns the current projection matrix.
### Return value

Current projection matrix
## void setReflectionViewportMask ( int mask )

Sets a new bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective surfaces match this one.
### Arguments

- *int* **mask** - The bit mask for rendering reflections into the viewport

## int getReflectionViewportMask () const

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective surfaces match this one.
### Return value

Current bit mask for rendering reflections into the viewport
## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. A node is rendered in the sprite viewport if its mask matches this one.
### Arguments

- *int* **mask** - The bit mask for rendering into the viewport

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. A node is rendered in the sprite viewport if its mask matches this one.
### Return value

Current bit mask for rendering into the viewport
## void setTextureHeight ( int height )

Sets a new height of the texture buffer used for the widget. This affects the widget size accordingly.
### Arguments

- *int* **height** - The height of the texture buffer used for the widget

## int getTextureHeight () const

Returns the current height of the texture buffer used for the widget. This affects the widget size accordingly.
### Return value

Current height of the texture buffer used for the widget
## void setTextureWidth ( int width )

Sets a new width of the texture buffer used for the widget.
### Arguments

- *int* **width** - The width of the texture buffer used for the widget

## int getTextureWidth () const

Returns the current width of the texture buffer used for the widget.
### Return value

Current width of the texture buffer used for the widget
## void setAspectCorrection ( int correction )

Sets a new value indicating if aspect correction is enabled for the sprite node.
### Arguments

- *int* **correction** - The aspect correction for the sprite node

## int isAspectCorrection () const

Returns the current value indicating if aspect correction is enabled for the sprite node.
### Return value

Current aspect correction for the sprite node
## void setUseTAAOffset ( int taaoffset )

Sets a new value indicating if skipping the render mode check is enabled to use TAA. It can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Arguments

- *int* **taaoffset** - The skipping of the render mode check to use TAA

## int isUseTAAOffset () const

Returns the current value indicating if skipping the render mode check is enabled to use TAA. It can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Return value

Current skipping of the render mode check to use TAA
---

## static WidgetSpriteNode ( Gui gui , int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## static WidgetSpriteNode ( int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the Engine GUI.
### Arguments

- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## void setCamera ( Camera camera )

Copies parameters of the given Camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera to be copied.

## void appendSkipFlags ( int flags )

Appends a new [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) without rewriting already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## int checkSkipFlags ( int flags )

Checks if given flags are already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

### Return value

**1** if flag/flags already set, otherwise **0**.
## void removeSkipFlags ( int flags )

Removes the given skip flag without affecting other set flags.
### Arguments

- *int* **flags** - A [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) to be removed. Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## void renderTexture ( Texture texture )

Renders the sprite node into the specified target texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target texture.
