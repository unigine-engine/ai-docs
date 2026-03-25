# Unigine::WidgetSpriteNode Class (CS)

**Inherits from:** WidgetSprite


This class is used to display separate nodes together with all their children. This widget supports alpha channel masking. But unlike [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md), it does not support engine postprocesses (like HDR, DOF, motion blur, glow, etc.); only [postprocess materials](../../../content/materials/library/postprocess/index.md) can be applied to it.


## WidgetSpriteNode Class

### Properties

## Node Node

The node set for displaying.
## float IFps

The frame duration used to render WidgetSpriteNode viewport.
## int LightUsage

The type of lighting for the WidgetSpriteNode.
## int SkipFlags

The [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_SHADOWS) set for the current viewport.
## string EnvironmentTexturePath

The path of the Environment texture.
## mat4 Modelview

The model-view matrix.
## mat4 Projection

The projection matrix.
## int ReflectionViewportMask

The bit mask for rendering reflections into the viewport. Reflections are rendered in the sprite viewport if masks of reflective materials match this one (one bit at least).
## int ViewportMask

The bit mask for rendering into the viewport. Node is rendered in the sprite viewport if its mask matches this one.
## int TextureHeight

The height of the texture buffer used for a widget that affects the widget size.
## int TextureWidth

The width of the texture buffer used for a widget that affects the widget size.
## bool AspectCorrection

The value indicating if the aspect correction enabled for WidgetSpriteNode.
## bool UseTAAOffset

The value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cs.md#RENDER_DEPTH).
### Members

---

## WidgetSpriteNode ( Gui gui , int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new sprite will belong.
- *int* **width** - Width of the sprite.
- *int* **height** - Height of the sprite.

## WidgetSpriteNode ( int width , int height )

Constructor. Creates a new sprite with given properties and adds it to the Engine GUI.
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
## void SetUseTAAOffset ( bool offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cs.md#RENDER_DEPTH).
### Arguments

- *bool* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## bool IsUseTAAOffset ( )

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cs.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
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

Renders the sprite node into the specified target texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target texture.
