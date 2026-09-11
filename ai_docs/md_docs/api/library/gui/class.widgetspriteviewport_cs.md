# Unigine::WidgetSpriteViewport Class (CS)

**Inherits from:** WidgetSprite


This class is used to create virtual monitors that display data from arbitrary cameras in the world. This widget is used to render the whole scene, with all engine post-processes like HDR, DOF, motion blur, glow, etc. Unlike [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_cs.md), this widget does not support alpha channel masking.


> **Notice:** By default, the sprite viewport is rendered at the same frame rate as the main Unigine viewport. For it to be rendered at different frame rate (for example, lower one in order to decrease the rendering load), use [*setIFps()*](#setIFps_float_void).


### See Also


- C++ sample
- UnigineScript sample


## WidgetSpriteViewport Class

### Properties

## float IFps

The constant frame duration used to render the sprite viewport, in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead. It can be used to decrease the frame rate to get higher performance (for example, if the widget is used to create a TV set, lowered frame rate makes no visual difference, but allows for faster rendering of the scene).
## int SkipFlags

The [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) set for the current viewport. Available flags:
- SKIP_SHADOWS
- SKIP_VISUALIZER
- SKIP_POSTEFFECTS
- SKIP_DYNAMIC_REFLECTIONS
- SKIP_VELOCITY_BUFFER
- SKIP_SRGB

## mat4 Modelview

The model-view matrix of the associated camera.
## mat4 Projection

The projection matrix of the associated camera.
## int ReflectionViewportMask

The bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective surfaces match this one.
## int ViewportMask

The bit mask for rendering into the viewport. Nodes are rendered in the sprite viewport if their masks match this one.
## int TextureHeight

The height of the texture buffer used for the widget. This affects the widget size accordingly.
## int TextureWidth

The width of the texture buffer used for the widget.
## bool AspectCorrection

The value indicating if aspect correction is enabled for the sprite viewport.
## bool UseTAAOffset

The value indicating if skipping the render mode check is enabled to use TAA. It can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cs.md#RENDER_DEPTH).
### Members

---

## WidgetSpriteViewport ( Gui gui , int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## WidgetSpriteViewport ( int width , int height )

Constructor. Creates a new viewport sprite with given properties and adds it to the Engine GUI.
### Arguments

- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## void SetCamera ( Camera camera )

Copies parameters of the given Camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera to be copied.

## Camera GetCamera ( )

Copies the instance of camera.
### Return value

Camera instance.
## void AppendSkipFlags ( int flags )

Appends a new [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) without rewriting already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## int CheckSkipFlags ( int flags )

Checks if given flags are already set.
### Arguments

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

### Return value

**1** if flag/flags already set, otherwise **0**.
## void RemoveSkipFlags ( int flags )

Removes the given skip flag without affecting other set flags.
### Arguments

- *int* **flags** - A [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) to be removed. Available flags:

  - SKIP_SHADOWS
  - SKIP_VISUALIZER
  - SKIP_POSTEFFECTS
  - SKIP_DYNAMIC_REFLECTIONS
  - SKIP_VELOCITY_BUFFER
  - SKIP_SRGB

## void RenderTexture ( Texture texture )

Renders the sprite viewport into the specified target texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target texture.
