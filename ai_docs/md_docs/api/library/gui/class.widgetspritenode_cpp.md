# Unigine::WidgetSpriteNode Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetSprite


This class is used to display separate nodes together with all their children. This widget supports alpha channel masking. But unlike [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md), it does not support engine postprocesses (like HDR, DOF, motion blur, glow, etc.); only [postprocess materials](../../../content/materials/library/postprocess/index.md) can be applied to it.


## WidgetSpriteNode Class

### Members

---

## static WidgetSpriteNodePtr create ( const Ptr < Gui > & gui , int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## static WidgetSpriteNodePtr create ( int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the Engine GUI.
### Arguments

- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## void setAspectCorrection ( bool correction )

Sets the aspect correction for the WidgetSpriteNode. true enables correction, false disables.
### Arguments

- *bool* **correction** - true to enable aspect correction, false to disable.

## bool isAspectCorrection ( ) const

Returns the value indicating if the aspect correction enabled for WidgetSpriteNode.
### Return value

true if the aspect correction enabled, otherwise false.
## void setCamera ( const Ptr < Camera > & camera )

Copies parameters of the given Camera instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera to be copied.

## Ptr < Camera > getCamera ( ) const

Copies the instance of camera.
### Return value

Camera instance.
## void setEnvironmentTexturePath ( const char * path )

Sets the given path for Environment texture.
### Arguments

- *const char ** **path** - Texture path to be set.

## const char * getEnvironmentTexturePath ( ) const

Returns the path of the Environment texture.
### Return value

Texture path.
## void setIFps ( float ifps )

Sets a constant frame duration used to render WidgetSpriteNode viewport. For example, it can be used to decrease the frame rate to get higher performance.
### Arguments

- *float* **ifps** - Frame duration in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead.

## float getIFps ( ) const

Returns the current frame duration used to render WidgetSpriteNode viewport.
### Return value

Frame duration in seconds (*1/FPS*).
## void setLightUsage ( int usage )

Sets the type of the lighting for the WidgetSpriteNode.
### Arguments

- *int* **usage** - The lighting type. Can be one of the following:

  - [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_WORLD_LIGHT)
  - [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_AUX_LIGHT)
  - [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_NODE_LIGHT)

## int getLightUsage ( ) const

Returns the type of lighting for the WidgetSpriteNode.
### Return value

The lighting type. Can be one of the following:
- [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_WORLD_LIGHT)
- [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_AUX_LIGHT)
- [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_cpp.md#USAGE_NODE_LIGHT)


## void setModelview ( const Math:: Mat4 & modelview )

Sets a model-view matrix.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **modelview** - Model-view matrix.

## Math:: Mat4 getModelview ( ) const

Returns the current model-view matrix.
### Return value

Model-view matrix.
## void setNode ( const Ptr < Node > & node )

Sets a node to be displayed.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node.

## Ptr < Node > getNode ( ) const

Returns the current node set for displaying.
### Return value

The node.
## void setProjection ( const Math:: mat4 & projection )

Sets a projection matrix.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix.

## Math:: mat4 getProjection ( ) const

Returns the current projection matrix.
### Return value

Projection matrix.
## void setReflectionViewportMask ( int mask )

Sets a bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective materials match this one (one bit at least).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getReflectionViewportMask ( ) const

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective materials match this one (one bit at least).
### Return value

Integer, each bit of which is a mask.
## void setSkipFlags ( int flags )

Sets the [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) for the WidgetSpriteViewport viewport.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## int getSkipFlags ( ) const

Returns the [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) set for the current viewport.
### Return value

A [skip flag.](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB


## void setTextureHeight ( int height )

Sets the height of the texture buffer used for a widget. This affects the widget size accordingly.
### Arguments

- *int* **height** - Height of the texture buffer size.

## int getTextureHeight ( ) const

Returns the height of the texture buffer used for a widget that affects the widget size.
### Return value

Height of the texture buffer size.
## void setTextureWidth ( int width )

Sets the width of the texture buffer used for a widget. This affects the widget size accordingly.
### Arguments

- *int* **width** - Width of the texture buffer size.

## int getTextureWidth ( ) const

Returns the width of the texture buffer used for a widget that affects the widget size.
### Return value

Width of the texture buffer size.
## void setUseTAAOffset ( bool offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Arguments

- *bool* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## bool isUseTAAOffset ( ) const

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Node is rendered in the sprite viewport if its mask matches this one.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getViewportMask ( ) const

Returns the current bit mask for rendering into the viewport. Node is rendered in the sprite viewport if its mask matches this one.
### Return value

Integer, each bit of which is a mask.
## void appendSkipFlags ( int flags )

Appends a new [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) without rewriting already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## int checkSkipFlags ( int flags )

Checks if given flags are already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) Available flags:

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

- *int* **flags** - A [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) to be removed. Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## void renderTexture ( const Ptr < Texture > & texture )

Renders the sprite node into the specified target texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target texture.
