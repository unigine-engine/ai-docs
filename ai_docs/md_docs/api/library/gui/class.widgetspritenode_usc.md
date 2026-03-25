# Unigine::WidgetSpriteNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetSprite


This class is used to display separate nodes together with all their children. This widget supports alpha channel masking. But unlike [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md), it does not support engine postprocesses (like HDR, DOF, motion blur, glow, etc.); only [postprocess materials](../../../content/materials/library/postprocess/index.md) can be applied to it.


## WidgetSpriteNode Class

### Members

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

## void setAspectCorrection ( int correction )

Sets the aspect correction for the WidgetSpriteNode. true enables correction, false disables.
### Arguments

- *int* **correction** - **1** to enable aspect correction, **0** to disable.

## int isAspectCorrection ( )

Returns the value indicating if the aspect correction enabled for WidgetSpriteNode.
### Return value

**1** if the aspect correction enabled, otherwise **0**.
## void setCamera ( Camera camera )

Copies parameters of the given Camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera to be copied.

## void setEnvironmentTexturePath ( string path )

Sets the given path for Environment texture.
### Arguments

- *string* **path** - Texture path to be set.

## string getEnvironmentTexturePath ( )

Returns the path of the Environment texture.
### Return value

Texture path.
## void setIFps ( float ifps )

Sets a constant frame duration used to render WidgetSpriteNode viewport. For example, it can be used to decrease the frame rate to get higher performance.
### Arguments

- *float* **ifps** - Frame duration in seconds (*1/FPS*). If a too small value is provided, **1E-6** will be used instead.

## float getIFps ( )

Returns the current frame duration used to render WidgetSpriteNode viewport.
### Return value

Frame duration in seconds (*1/FPS*).
## void setLightUsage ( int usage )

Sets the type of the lighting for the WidgetSpriteNode.
### Arguments

- *int* **usage** - The lighting type. Can be one of the following:

  - [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_WORLD_LIGHT)
  - [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_AUX_LIGHT)
  - [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_NODE_LIGHT)

## int getLightUsage ( )

Returns the type of lighting for the WidgetSpriteNode.
### Return value

The lighting type. Can be one of the following:
- [USAGE_WORLD_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_WORLD_LIGHT)
- [USAGE_AUX_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_AUX_LIGHT)
- [USAGE_NODE_LIGHT](../../../api/library/rendering/class.viewport_usc.md#USAGE_NODE_LIGHT)


## void setModelview ( Mat4 modelview )

Sets a model-view matrix.
### Arguments

- *Mat4* **modelview** - Model-view matrix.

## Mat4 getModelview ( )

Returns the current model-view matrix.
### Return value

Model-view matrix.
## void setNode ( Node node )

Sets a node to be displayed.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node.

## Node getNode ( )

Returns the current node set for displaying.
### Return value

The node.
## void setProjection ( mat4 projection )

Sets a projection matrix.
### Arguments

- *mat4* **projection** - Projection matrix.

## mat4 getProjection ( )

Returns the current projection matrix.
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

- *int* **flags** - A [skip flag.](../../../api/library/rendering/class.viewport_usc.md#SKIP_SHADOWS) Available flags:

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
## void setUseTAAOffset ( int offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Arguments

- *int* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## int isUseTAAOffset ( )

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Node is rendered in the sprite viewport if its mask matches this one.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getViewportMask ( )

Returns the current bit mask for rendering into the viewport. Node is rendered in the sprite viewport if its mask matches this one.
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

Renders the sprite node into the specified target texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target texture.
