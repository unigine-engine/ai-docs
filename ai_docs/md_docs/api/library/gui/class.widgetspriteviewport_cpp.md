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

## void setIFps ( float ifps )

Sets a new constant frame duration used to render the sprite viewport, in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead. It can be used to decrease the frame rate to get higher performance (for example, if the widget is used to create a TV set, lowered frame rate makes no visual difference, but allows for faster rendering of the scene).
### Arguments

- *float* **ifps** - The constant frame duration used to render the sprite viewport

## float getIFps () const

Returns the current constant frame duration used to render the sprite viewport, in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead. It can be used to decrease the frame rate to get higher performance (for example, if the widget is used to create a TV set, lowered frame rate makes no visual difference, but allows for faster rendering of the scene).
### Return value

Current constant frame duration used to render the sprite viewport
## void setSkipFlags ( int flags )

Sets a new [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) set for the current viewport. Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB

### Arguments

- *int* **flags** - The skip flags set for the current viewport

## int getSkipFlags () const

Returns the current [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_SHADOWS) set for the current viewport. Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB

### Return value

Current skip flags set for the current viewport
## void setModelview ( const Math:: Mat4 & modelview )

Sets a new model-view matrix of the associated camera.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **modelview** - The model-view matrix of the associated camera

## Math:: Mat4 getModelview () const

Returns the current model-view matrix of the associated camera.
### Return value

Current model-view matrix of the associated camera
## void setProjection ( const Math:: mat4 & projection )

Sets a new projection matrix of the associated camera.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **projection** - The projection matrix of the associated camera

## Math:: mat4 getProjection () const

Returns the current projection matrix of the associated camera.
### Return value

Current projection matrix of the associated camera
## void setReflectionViewportMask ( int mask )

Sets a new bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective surfaces match this one.
### Arguments

- *int* **mask** - The bit mask for rendering reflections into the viewport

## int getReflectionViewportMask () const

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective surfaces match this one.
### Return value

Current bit mask for rendering reflections into the viewport
## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. Nodes are rendered in the sprite viewport if their masks match this one.
### Arguments

- *int* **mask** - The bit mask for rendering into the viewport

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. Nodes are rendered in the sprite viewport if their masks match this one.
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
## void setAspectCorrection ( bool correction )

Sets a new value indicating if aspect correction is enabled for the sprite viewport.
### Arguments

- *bool* **correction** - Set **true** to enable aspect correction for the sprite viewport; **false** - to disable it.

## bool isAspectCorrection () const

Returns the current value indicating if aspect correction is enabled for the sprite viewport.
### Return value

**true** if aspect correction for the sprite viewport is enabled ; otherwise **false**.
## void setUseTAAOffset ( bool taaoffset )

Sets a new value indicating if skipping the render mode check is enabled to use TAA. It can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Arguments

- *bool* **taaoffset** - Set **true** to enable skipping of the render mode check to use TAA; **false** - to disable it.

## bool isUseTAAOffset () const

Returns the current value indicating if skipping the render mode check is enabled to use TAA. It can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Return value

**true** if skipping of the render mode check to use TAA is enabled ; otherwise **false**.
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

## void setCamera ( const Ptr < Camera > & camera )

Copies parameters of the given Camera instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera to be copied.

## Ptr < Camera > getCamera ( ) const

Copies the instance of camera.
### Return value

Camera instance.
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
