# Unigine::WidgetSpriteViewport Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetSprite


This class is used to create virtual monitors that display data from arbitrary cameras in the world. This widget is used to render the whole scene, with all engine post-processes like HDR, DOF, motion blur, glow, etc. Unlike [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_cpp.md), this widget does not support alpha channel masking.


> **Notice:** By default, the sprite viewport is rendered at the same frame rate as the main Unigine viewport. For it to be rendered at different frame rate (for example, lower one in order to decrease the rendering load), use [*setIFps()*](#setIFps_float_void).


### See Also


- C++ sample
- UnigineScript sample


## WidgetSpriteViewport Class

### Members

---

## static WidgetSpriteViewportPtr create ( const Ptr < Gui > & gui , int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## static WidgetSpriteViewportPtr create ( int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the Engine GUI.
### Arguments

- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## void setAspectCorrection ( bool correction )

Sets the aspect correction for the WidgetSpriteViewport. true enables correction, false disables.
### Arguments

- *bool* **correction** - true to enable aspect correction, false to disable.

## bool isAspectCorrection ( ) const

Returns the value indicating if the aspect correction enabled for WidgetSpriteViewport.
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
## void setIFps ( float ifps )

Sets a constant frame duration used to render sprite viewport. It can be used to decrease the frame rate to get higher performance. (For example, if the widget is used to create a TV set, lowered frame rate makes no visual difference, but allows for faster rendering of the scene.)
### Arguments

- *float* **ifps** - Frame duration in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead. **0** means that a widget is rendered at the same frame rate as the main application window.

## float getIFps ( ) const

Returns the current constant frame duration used to render WidgetSpriteViewport viewport.
### Return value

Frame duration in seconds (1 / FPS).
## void setModelview ( const Math:: Mat4 & modelview )

Sets a model-view matrix for the associated camera.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **modelview** - Model-view matrix.

## Math:: Mat4 getModelview ( ) const

Returns the current model-view matrix of the associated camera.
### Return value

Model-view matrix.
## void setProjection ( const Math:: mat4 & projection )

Sets a projection matrix for the associated camera.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix.

## Math:: mat4 getProjection ( ) const

Returns the current projection matrix of the associated camera.
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

- *int* **flags** - A [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS). Available flags:

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
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Nodes are rendered in this sprite viewport if their masks match this one.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getViewportMask ( ) const

Returns the current bit mask for rendering into the viewport. Nodes are rendered in the sprite viewport if their masks match this one.
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

Renders the sprite viewport into the specified target texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target texture.

## void setUseTAAOffset ( bool offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Arguments

- *bool* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## bool isUseTAAOffset ( ) const

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
