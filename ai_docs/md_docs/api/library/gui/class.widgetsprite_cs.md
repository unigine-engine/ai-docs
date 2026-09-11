# Unigine::WidgetSprite Class (CS)

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

### Properties

## string Texture

The texture from a file set for the first (bottom) layer of the sprite.
## mat4 Transform

The transformation matrix set for the first (bottom) layer of the sprite.
## vec4 TexCoord

The coordinates of the texture set for the first (bottom) layer of the sprite.
## 🔒︎ int BlendDestFunc

The blending mode of the destination widget colour set for the first (bottom) layer of the sprite. One of the [BLEND_*](../../../api/library/gui/class.gui_cs.md) values.
## 🔒︎ int BlendSrcFunc

The blending mode of the source screen buffer colour set for the first (bottom) layer of the sprite. One of the [BLEND_*](../../../api/library/gui/class.gui_cs.md) values.
## int BufferMask

The channel mask for the whole sprite. One of the [GUI_BUFFER_*](../../../api/library/gui/class.gui_cs.md) values.
## int WrapRepeat

The value indicating if texture tiling is enabled for the first (bottom) layer of the sprite. This layer always exists in the sprite. The default is 0 (no tiling). To see tiling in effect, you need to transform sprite texture coordinates via [setTexCoord()](#setTexCoord_vec4_void).
## vec4 Color

The color set for the first (bottom) layer of the sprite.
## 🔒︎ int NumLayers

The total number of layers in the sprite.
## float IntersectionImageThreshold

The threshold value for the pixel. If the pixel value in the intersection mask is higher than the threshold, the intersection is detected.
## mat4 IntersectionImageTransform

The transformation for the image used as a mask for defining intersections with the mouse.
## bool IntersectionImageEnabled

The value indicating if the intersection image is used as a mask for detecting intersections with the mouse.
### Members

---

## WidgetSprite ( Gui gui , string name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new sprite will belong.
- *string* **name** - Path to the texture. This is an optional parameter.

## WidgetSprite ( string name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the Engine GUI.
### Arguments

- *string* **name** - Path to the texture. This is an optional parameter.

## void SetBlendFunc ( int src , int dest )

Sets blending coefficients for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *int* **src** - Blending mode for the source screen buffer color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination widget color (one of the *[GUI_BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).

## void SetImage ( Image image , int dynamic = 0 )

Sets a loaded into memory image for the first (bottom) layer of the sprite. This layer always exists in the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* !

### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Pointer to the image.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Image GetImage ( )

Returns the loaded into memory image that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* !

### Return value

Pointer to the image.
## int GetLayerBlendDestFunc ( int layer )

Returns the blending mode of the destination widget colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).
## void SetLayerBlendFunc ( int layer , int src , int dest )

Sets blending coefficients for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **src** - Blending mode for the source color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).

## int GetLayerBlendSrcFunc ( int layer )

Returns the blending mode of the source screen buffer colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[BLEND_*](../../../api/library/gui/class.gui_cs.md#BLEND_DEST_ALPHA)* variables).
## void SetLayerBufferMask ( int layer , int mask )

Sets a channel mask for a given layer of the sprite. If a mask for a channel exists, one can draw in this channel. The default is [*BUFFER_ALL*](../../../api/library/gui/class.gui_cs.md#BUFFER_ALL).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **mask** - Channel mask. One of the [*BUFFER_**](../../../api/library/gui/class.gui_cs.md#BUFFER_ALL) pre-defined variables.

## int GetLayerBufferMask ( int layer )

Returns the current channel mask set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Channel mask. One of the [*BUFFER_**](../../../api/library/gui/class.gui_cs.md#BUFFER_ALL) pre-defined variables.
## void SetLayerColor ( int layer , vec4 color )

Sets a color for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *vec4* **color** - Modulation color.

## vec4 GetLayerColor ( int layer )

Returns the current color set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Modulation color.
## void SetLayerEnabled ( int layer , bool enabled )

Sets a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *bool* **enabled** - true to enable the layer; false to disable it.

## int IsLayerEnabled ( int layer )

Returns a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

1 if the layer is enabled; 0 if disabled.
## int GetLayerHeight ( int layer )

Returns the current width of the layer (regardless of layer transformation).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Width of the layer in units.
## void SetLayerImage ( int layer , Image image , int dynamic = 0 )

Sets an image for a given layer of the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Image GetLayerImage ( int layer )

Returns the current image set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Current image set for the specified sprite layer.
## void SetLayerRender ( int layer , Texture texture , int flipped = 0 )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Texture GetLayerRender ( int layer )

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Pointer to the texture.
## void SetLayerTexCoord ( int layer , vec4 texcoord )

Sets the coordinates of the texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *vec4* **texcoord** - Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.

## vec4 GetLayerTexCoord ( int layer )

Returns the current coordinates of the texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.
## void SetLayerTexture ( int layer , string name )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *string* **name** - Path to the texture.

## string GetLayerTexture ( int layer )

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Path to the texture.
## void SetLayerTransform ( int layer , mat4 transform )

Sets a transformation matrix for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *mat4* **transform** - Transformation matrix.

## mat4 GetLayerTransform ( int layer )

Returns the current transformation matrix set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Transformation matrix.
## int GetLayerWidth ( int layer )

Returns the current width of the layer (regardless of layer transformation).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Width of the layer in units.
## void SetLayerWrapRepeat ( int layer , int repeat )

Sets texture tiling for a given layer of the sprite.
> **Notice:** To see tiling in effect, you need to transform sprite texture coordinates via **[SetLayerTexCoord()](../../...md#setLayerTexCoord_int_vec4_void)**.

### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **repeat** - Positive number to enable texture tiling; 0 to disable it.

## int GetLayerWrapRepeat ( int layer )

Returns a value indicating if texture tiling is enabled for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

true if texture tiling is enabled; false if disabled.
## void SetRender ( Texture texture , int flipped = 0 )

Sets a texture to be rendered for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* !

### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Texture GetRender ( )

Returns the pointer to the texture that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* !

### Return value

Pointer to the texture.
## int AddLayer ( )

Adds an empty layer with default properties to the sprite.
### Return value

Number of the added layer.
## void RemoveLayer ( int layer )

Removes a given layer from the sprite.
### Arguments

- *int* **layer** - Layer number.

## void SetIntersectionImage ( Image image )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be used as a mask for defining intersections.

## void SetIntersectionImageName ( string name )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *string* **name** - Name of the image to be used as a mask for defining intersections.

## Image GetIntersectionImage ( )

Returns the image used as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Return value

Image to be used as a mask for defining intersections.
