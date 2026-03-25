# Unigine::WidgetSpriteViewport Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetSprite


This class is used to create virtual monitors that display data from arbitrary cameras in the world. This widget is used to render the whole scene, with all engine post-processes like HDR, DOF, motion blur, glow, etc. Unlike [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_usc.md), this widget does not support alpha channel masking.


> **Notice:** By default, the sprite viewport is rendered at the same frame rate as the main Unigine viewport. For it to be rendered at different frame rate (for example, lower one in order to decrease the rendering load), use [*setIFps()*](#setIFps_float_void).


### See Also


- C++ sample
- UnigineScript sample


## WidgetSpriteViewport Class

### Members

---

## static WidgetSpriteViewport ( Gui gui , int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## static WidgetSpriteViewport ( int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the Engine GUI.
### Arguments

- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## void setAspectCorrection ( int correction )

Sets the aspect correction for the WidgetSpriteViewport. true enables correction, false disables.
### Arguments

- *int* **correction** - **1** to enable aspect correction, **0** to disable.

## int isAspectCorrection ( )

Returns the value indicating if the aspect correction enabled for WidgetSpriteViewport.
### Return value

**1** if the aspect correction enabled, otherwise **0**.
## void setCamera ( Camera camera )

Copies parameters of the given Camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera to be copied.

## getCamera ( )

Copies the instance of camera.
### Return value

Camera instance.
## void setIFps ( float ifps )

Sets a constant frame duration used to render sprite viewport. It can be used to decrease the frame rate to get higher performance. (For example, if the widget is used to create a TV set, lowered frame rate makes no visual difference, but allows for faster rendering of the scene.)
### Arguments

- *float* **ifps** - Frame duration in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead. **0** means that a widget is rendered at the same frame rate as the main application window.

## float getIFps ( )

Returns the current constant frame duration used to render WidgetSpriteViewport viewport.
### Return value

Frame duration in seconds (1 / FPS).
## void setModelview ( Mat4 modelview )

Sets a model-view matrix for the associated camera.
### Arguments

- *Mat4* **modelview** - Model-view matrix.

## Mat4 getModelview ( )

Returns the current model-view matrix of the associated camera.
### Return value

Model-view matrix.
## void setProjection ( mat4 projection )

Sets a projection matrix for the associated camera.
### Arguments

- *mat4* **projection** - Projection matrix.

## mat4 getProjection ( )

Returns the current projection matrix of the associated camera.
### Return value

Projection matrix.
## void setReflectionViewportMask ( int mask )

Sets a bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective materials match this one (one bit at least).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getReflectionViewportMask ( )

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective materials match this one (one bit at least).
### Return value

Integer, each bit of which is a mask.
## void setSkipFlags ( int flags )

Sets the [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) for the WidgetSpriteViewport viewport.
### Arguments

- *int* **flags** - A [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS). Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## int getSkipFlags ( )

Returns the [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) set for the current viewport.
### Return value

A [skip flag.](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) Available flags:
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

## int getTextureHeight ( )

Returns the height of the texture buffer used for a widget that affects the widget size.
### Return value

Height of the texture buffer size.
## void setTextureWidth ( int width )

Sets the width of the texture buffer used for a widget. This affects the widget size accordingly.
### Arguments

- *int* **width** - Width of the texture buffer size.

## int getTextureWidth ( )

Returns the width of the texture buffer used for a widget that affects the widget size.
### Return value

Width of the texture buffer size.
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Nodes are rendered in this sprite viewport if their masks match this one.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getViewportMask ( )

Returns the current bit mask for rendering into the viewport. Nodes are rendered in the sprite viewport if their masks match this one.
### Return value

Integer, each bit of which is a mask.
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

Renders the sprite viewport into the specified target texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target texture.

## void setUseTAAOffset ( int offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Arguments

- *int* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## int isUseTAAOffset ( )

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
