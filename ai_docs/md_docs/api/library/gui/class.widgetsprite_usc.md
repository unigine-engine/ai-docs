# Unigine::WidgetSprite Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This base class is used to create sprites, which are basically any widgets dealing with images.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/sprite.jpg)


A sprite has a background layer which is used to calculate a bounding box of the widget and in addition can have a number of layers. All layer including the bottom one can be assigned textures, tiled and blended.


> **Notice:** You can transform all layers, but avoid rotating a background layer. Being used to calculate a bounding box, it stretches if rotated. Rotate layers instead.


### See Also


- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
  -
- The [Widgets](../../../code/gui/ui/ui_widgets.md#sprite) article providing details on the sprite


## WidgetSprite Class

### Members

---

## static WidgetSprite ( Gui gui , string name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new sprite will belong.
- *string* **name** - Path to the texture. This is an optional parameter.

## static WidgetSprite ( string name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the Engine GUI.
### Arguments

- *string* **name** - Path to the texture. This is an optional parameter.

## int getBlendDestFunc ( )

Returns the blending mode of the destination widget colour set for the first (bottom) layer of the sprite.
### Return value

Blending mode (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
## void setBlendFunc ( int src , int dest )

Sets blending coefficients for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *int* **src** - Blending mode for the source screen buffer color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination widget color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).

## int getBlendSrcFunc ( )

Returns the blending mode of the source screen buffer colour set for the first (bottom) layer of the sprite.
### Return value

Blending mode (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
## void setBufferMask ( int mask )

Sets a channel mask for the whole sprite. If a mask for a channel exists, one can draw in this channel. The default is [*GUI_BUFFER_ALL*](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL).
### Arguments

- *int* **mask** - Current channel mask (one of the *[GUI_BUFFER_*](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL)* pre-defined variables).

## int getBufferMask ( )

Returns the current channel mask for the whole sprite.
### Return value

Current channel mask (one of the *[GUI_BUFFER_*](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL)* pre-defined variables).
## void setColor ( vec4 color )

Sets a color for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *vec4* **color** - Modulation color.

## vec4 getColor ( )

Returns the current color set for the first (bottom) layer of the sprite.
### Return value

Modulation color.
## void setImage ( int dynamic = 0 )

Sets a loaded into memory image for the first (bottom) layer of the sprite. This layer always exists in the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md)* !

### Arguments

- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Image getImage ( )

Returns the loaded into memory image that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md)* !

### Return value

Pointer to the image.
## int getLayerBlendDestFunc ( int layer )

Returns the blending mode of the destination widget colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
## void setLayerBlendFunc ( int layer , int src , int dest )

Sets blending coefficients for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **src** - Blending mode for the source color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).

## int getLayerBlendSrcFunc ( int layer )

Returns the blending mode of the source screen buffer colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_usc.md#BLEND_DEST_ALPHA)* variables).
## void setLayerBufferMask ( int layer , int mask )

Sets a channel mask for a given layer of the sprite. If a mask for a channel exists, one can draw in this channel. The default is [*GUI_BUFFER_ALL*](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **mask** - One of the [*GUI_BUFFER_**](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL) pre-defined variables.

## int getLayerBufferMask ( int layer )

Returns the current channel mask set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

One of the [*GUI_BUFFER_**](../../../api/library/gui/class.gui_usc.md#BUFFER_ALL) pre-defined variables.
## void setLayerColor ( int layer , vec4 color )

Sets a color for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *vec4* **color** - Modulation color.

## vec4 getLayerColor ( int layer )

Returns the current color set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Modulation color.
## void setLayerEnabled ( int layer , int enabled )

Sets a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **enabled** - **1** to enable the layer; **0** to disable it.

## int isLayerEnabled ( int layer )

Returns a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

**1** if the layer is enabled; **0** if disabled.
## int getLayerHeight ( int layer )

Returns the current height of the layer (regardless of [layer transformation](#setLayerTransform_int_mat4_void)).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Height of the layer in units.
## void setLayerImage ( int layer , Image image , int dynamic = 0 )

Sets an image for a given layer of the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Image getLayerImage ( int layer )

Returns the current image set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Current image set for the specified sprite layer.
## void setLayerRender ( int layer , Texture texture , int flipped = 0 )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Texture getLayerRender ( int layer )

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Pointer to the texture.
## void setLayerTexCoord ( int layer , vec4 texcoord )

Sets the coordinates of the texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *vec4* **texcoord** - Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.

## vec4 getLayerTexCoord ( int layer )

Returns the current coordinates of the texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.
## void setLayerTexture ( int layer , string name )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *string* **name** - Path to the texture.

## string getLayerTexture ( int layer )

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Path to the texture.
## void setLayerTransform ( int layer , mat4 transform )

Sets a transformation matrix for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *mat4* **transform** - Transformation matrix.

## mat4 getLayerTransform ( int layer )

Returns the current transformation matrix set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Transformation matrix.
## int getLayerWidth ( int layer )

Returns the current width of the layer (regardless of layer transformation).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Width of the layer in units.
## void setLayerWrapRepeat ( int layer , int repeat )

Sets texture tiling for a given layer of the sprite.
> **Notice:** To see tiling in effect, you need to transform sprite texture coordinates via **[setLayerTexCoord()()](../../...md#setLayerTexCoord_int_vec4_void)**.

### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **repeat** - Positive number to enable texture tiling; 0 to disable it.

## int getLayerWrapRepeat ( int layer )

Returns a value indicating if texture tiling is enabled for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

**1** if texture tiling is enabled; **0** if disabled.
## int getNumLayers ( )

Returns the total number of layers in the sprite.
### Return value

Number of layers.
## void setRender ( Texture texture , int flipped = 0 )

Sets a texture to be rendered for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md)* !

### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Texture getRender ( )

Returns the pointer to the texture that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_usc.md)* !

### Return value

Pointer to the texture.
## void setTexCoord ( vec4 coord )

Sets the coordinates of the texture for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *vec4* **coord** - Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.

## vec4 getTexCoord ( )

Returns the current coordinates of the texture set for the first (bottom) layer of the sprite.
### Return value

Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.
## void setTexture ( string texture )

Sets a texture from a file for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *string* **texture** - Path to the texture.

## string getTexture ( )

Returns the texture from a file that is currently set for the first (bottom) layer of the sprite.
### Return value

Path to the texture.
## void setTransform ( mat4 transform )

Sets a transformation matrix for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *mat4* **transform** - Transformation matrix.

## mat4 getTransform ( )

Returns the current transformation matrix set for the first (bottom) layer of the sprite.
### Return value

Transformation matrix.
## void setWrapRepeat ( int repeat )

Sets texture tiling for the first (bottom) layer of the sprite. This layer always exists in the sprite.
> **Notice:** To see tiling in effect, you need to transform sprite texture coordinates via *[setTexCoord()](#setTexCoord_vec4_void)*.


### Arguments

- *int* **repeat** - Positive number to enable texture tiling; **0** to disable it.

## int getWrapRepeat ( )

Returns a value indicating if texture tiling is enabled for the first (bottom) layer of the sprite.
### Return value

**1** if texture tiling is enabled; **0** if disabled.
## int addLayer ( )

Adds an empty layer with default properties to the sprite.
### Return value

Number of the added layer.
## void removeLayer ( int layer )

Removes a given layer from the sprite.
### Arguments

- *int* **layer** - Layer number.

## void setIntersectionImage ( Image image )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to be used as a mask for defining intersections.

## void setIntersectionImageName ( string name )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *string* **name** - Name of the image to be used as a mask for defining intersections.

## Image getIntersectionImage ( )

Returns the image used as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Return value

Image to be used as a mask for defining intersections.
## void setIntersectionImageTransform ( mat4 transform )

Sets the transformation for the image used as a mask for defining intersections with the mouse.
### Arguments

- *mat4* **transform** - Image transformation.

## mat4 getIntersectionImageTransform ( )

Returns the transformation for the image used as a mask for defining intersections with the mouse.
### Return value

Image transformation.
## void setIntersectionImageThreshold ( float threshold )

Sets the threshold value for the pixel. If the pixel value in the intersection mask is higher that the threshold, the intersection is detected.
### Arguments

- *float* **threshold** - Threshold value for the pixel.

## float getIntersectionImageThreshold ( )

Sets the threshold value for the pixel. If the pixel value in the intersection mask is higher that the threshold, the intersection is detected.
### Return value

Threshold value for the pixel.
## void setIntersectionImageEnabled ( int enabled = false )

Sets the flag defining if the intersection image is used as a mask for detecting intersections with the mouse.
### Arguments

- *int* **enabled** - **1** to enable the intersection image; **0** to disable it.

## int isIntersectionImageEnabled ( )

Returns the value showing if the intersection image is used as a mask for detecting intersections with the mouse.
### Return value

**1** if the intersection image is enabled; otherwise **0**.
