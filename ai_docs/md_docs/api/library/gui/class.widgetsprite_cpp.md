# Unigine::WidgetSprite Class (CPP)

**Header:** #include <UnigineWidgets.h>

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

## void setTexture ( const char * texture )

Sets a new texture from a file set for the first (bottom) layer of the sprite.
### Arguments

- *const char ** **texture** - The texture from a file set for the first (bottom) layer of the sprite

## const char * getTexture () const

Returns the current texture from a file set for the first (bottom) layer of the sprite.
### Return value

Current texture from a file set for the first (bottom) layer of the sprite
## void setTransform ( const Math:: mat4 & transform )

Sets a new transformation matrix set for the first (bottom) layer of the sprite.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix set for the first (bottom) layer of the sprite

## Math:: mat4 getTransform () const

Returns the current transformation matrix set for the first (bottom) layer of the sprite.
### Return value

Current transformation matrix set for the first (bottom) layer of the sprite
## void setTexCoord ( const Math:: vec4 & coord )

Sets a new coordinates of the texture set for the first (bottom) layer of the sprite.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **coord** - The coordinates of the texture set for the first (bottom) layer of the sprite

## Math:: vec4 getTexCoord () const

Returns the current coordinates of the texture set for the first (bottom) layer of the sprite.
### Return value

Current coordinates of the texture set for the first (bottom) layer of the sprite
## int getBlendDestFunc () const

Returns the current blending mode of the destination widget colour set for the first (bottom) layer of the sprite. One of the [BLEND_*](../../../api/library/gui/class.gui_cpp.md) values.
### Return value

Current blending mode of the destination widget colour for the first (bottom) layer
## int getBlendSrcFunc () const

Returns the current blending mode of the source screen buffer colour set for the first (bottom) layer of the sprite. One of the [BLEND_*](../../../api/library/gui/class.gui_cpp.md) values.
### Return value

Current blending mode of the source screen buffer colour for the first (bottom) layer
## void setBufferMask ( int mask )

Sets a new channel mask for the whole sprite. One of the [GUI_BUFFER_*](../../../api/library/gui/class.gui_cpp.md) values.
### Arguments

- *int* **mask** - The channel mask for the whole sprite

## int getBufferMask () const

Returns the current channel mask for the whole sprite. One of the [GUI_BUFFER_*](../../../api/library/gui/class.gui_cpp.md) values.
### Return value

Current channel mask for the whole sprite
## void setWrapRepeat ( int repeat )

Sets a new value indicating if texture tiling is enabled for the first (bottom) layer of the sprite. This layer always exists in the sprite. The default is 0 (no tiling). To see tiling in effect, you need to transform sprite texture coordinates via [setTexCoord()](#setTexCoord_vec4_void).
### Arguments

- *int* **repeat** - The flag indicating whether texture tiling is enabled for the first (bottom) layer of the sprite

## int getWrapRepeat () const

Returns the current value indicating if texture tiling is enabled for the first (bottom) layer of the sprite. This layer always exists in the sprite. The default is 0 (no tiling). To see tiling in effect, you need to transform sprite texture coordinates via [setTexCoord()](#setTexCoord_vec4_void).
### Return value

Current flag indicating whether texture tiling is enabled for the first (bottom) layer of the sprite
## void setColor ( const Math:: vec4 & color )

Sets a new color set for the first (bottom) layer of the sprite.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color set for the first (bottom) layer of the sprite

## Math:: vec4 getColor () const

Returns the current color set for the first (bottom) layer of the sprite.
### Return value

Current color set for the first (bottom) layer of the sprite
## int getNumLayers () const

Returns the current total number of layers in the sprite.
### Return value

Current total number of layers in the sprite
## void setIntersectionImageThreshold ( float threshold )

Sets a new threshold value for the pixel. If the pixel value in the intersection mask is higher than the threshold, the intersection is detected.
### Arguments

- *float* **threshold** - The threshold value for the pixel

## float getIntersectionImageThreshold () const

Returns the current threshold value for the pixel. If the pixel value in the intersection mask is higher than the threshold, the intersection is detected.
### Return value

Current threshold value for the pixel
## void setIntersectionImageTransform ( const Math:: mat4 & transform )

Sets a new transformation for the image used as a mask for defining intersections with the mouse.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation for the image used as an intersection mask

## Math:: mat4 getIntersectionImageTransform () const

Returns the current transformation for the image used as a mask for defining intersections with the mouse.
### Return value

Current transformation for the image used as an intersection mask
## void setIntersectionImageEnabled ( bool enabled )

Sets a new value indicating if the intersection image is used as a mask for detecting intersections with the mouse.
### Arguments

- *bool* **enabled** - Set **true** to enable use of the intersection image as a mask for detecting intersections with the mouse; **false** - to disable it.

## bool isIntersectionImageEnabled () const

Returns the current value indicating if the intersection image is used as a mask for detecting intersections with the mouse.
### Return value

**true** if use of the intersection image as a mask for detecting intersections with the mouse is enabled ; otherwise **false**.
---

## static WidgetSpritePtr create ( const Ptr < Gui > & gui , const char * name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new sprite will belong.
- *const char ** **name** - Path to the texture. This is an optional parameter.

## static WidgetSpritePtr create ( const char * name = 0 )

Constructor. Creates a sprite with a given texture and adds it to the Engine GUI.
### Arguments

- *const char ** **name** - Path to the texture. This is an optional parameter.

## void setBlendFunc ( int src , int dest )

Sets blending coefficients for the first (bottom) layer of the sprite. This layer always exists in the sprite.
### Arguments

- *int* **src** - Blending mode for the source screen buffer color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination widget color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).

## void setImage ( const Ptr < Image > & image , int dynamic = 0 )

Sets a loaded into memory image for the first (bottom) layer of the sprite. This layer always exists in the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* !

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Pointer to the image.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Ptr < Image > getImage ( ) const

Returns the loaded into memory image that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* !

### Return value

Pointer to the image.
## int getLayerBlendDestFunc ( int layer ) const

Returns the blending mode of the destination widget colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).
## void setLayerBlendFunc ( int layer , int src , int dest )

Sets blending coefficients for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **src** - Blending mode for the source color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).
- *int* **dest** - Blending mode for the destination color (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).

## int getLayerBlendSrcFunc ( int layer ) const

Returns the blending mode of the source screen buffer colour set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Blending mode (one of the *[BLEND_*](../../../api/library/gui/class.gui_cpp.md#BLEND_DEST_ALPHA)* variables).
## void setLayerBufferMask ( int layer , int mask )

Sets a channel mask for a given layer of the sprite. If a mask for a channel exists, one can draw in this channel. The default is [*BUFFER_ALL*](../../../api/library/gui/class.gui_cpp.md#BUFFER_ALL).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **mask** - Channel mask. One of the [*BUFFER_**](../../../api/library/gui/class.gui_cpp.md#BUFFER_ALL) pre-defined variables.

## int getLayerBufferMask ( int layer ) const

Returns the current channel mask set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Channel mask. One of the [*BUFFER_**](../../../api/library/gui/class.gui_cpp.md#BUFFER_ALL) pre-defined variables.
## void setLayerColor ( int layer , const Math:: vec4 & color )

Sets a color for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Modulation color.

## Math:: vec4 getLayerColor ( int layer ) const

Returns the current color set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers..

### Return value

Modulation color.
## void setLayerEnabled ( int layer , bool enabled )

Sets a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *bool* **enabled** - true to enable the layer; false to disable it.

## int isLayerEnabled ( int layer ) const

Returns a value indicating if the layer is enabled for rendering.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

1 if the layer is enabled; 0 if disabled.
## int getLayerHeight ( int layer ) const

Returns the current width of the layer (regardless of layer transformation).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Width of the layer in units.
## void setLayerImage ( int layer , const Ptr < Image > & image , int dynamic = 0 )

Sets an image for a given layer of the sprite. An additional flag can be set in case the sprite image is going to be updated often or even each frame (for optimized memory management).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Ptr < Image > getLayerImage ( int layer ) const

Returns the current image set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Current image set for the specified sprite layer.
## void setLayerRender ( int layer , const Ptr < Texture > & texture , int flipped = 0 )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Ptr < Texture > getLayerRender ( int layer ) const

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Pointer to the texture.
## void setLayerTexCoord ( int layer , const Math:: vec4 & texcoord )

Sets the coordinates of the texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **texcoord** - Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.

## Math:: vec4 getLayerTexCoord ( int layer ) const

Returns the current coordinates of the texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Texture coordinates. The first pair of coordinates (x and y) is for the upper left corner, the second pair (z and w) is for the lower right corner.
## void setLayerTexture ( int layer , const char * name )

Sets a texture for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const char ** **name** - Path to the texture.

## const char * getLayerTexture ( int layer ) const

Returns the current texture set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Path to the texture.
## void setLayerTransform ( int layer , const Math:: mat4 & transform )

Sets a transformation matrix for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: mat4 getLayerTransform ( int layer ) const

Returns the current transformation matrix set for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Transformation matrix.
## int getLayerWidth ( int layer ) const

Returns the current width of the layer (regardless of layer transformation).
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

Width of the layer in units.
## void setLayerWrapRepeat ( int layer , int repeat )

Sets texture tiling for a given layer of the sprite.
> **Notice:** To see tiling in effect, you need to transform sprite texture coordinates via **[setLayerTexCoord()](../../...md#setLayerTexCoord_int_vec4_void)**.

### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.
- *int* **repeat** - Positive number to enable texture tiling; 0 to disable it.

## int getLayerWrapRepeat ( int layer ) const

Returns a value indicating if texture tiling is enabled for a given layer of the sprite.
### Arguments

- *int* **layer** - Layer number in range from 0 to the total number of sprite layers.

### Return value

true if texture tiling is enabled; false if disabled.
## void setRender ( const Ptr < Texture > & texture , int flipped = 0 )

Sets a texture to be rendered for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* !

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Ptr < Texture > getRender ( ) const

Returns the pointer to the texture that is currently set for the first (bottom) layer of the sprite.
> **Warning:** Not available for the *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* !

### Return value

Pointer to the texture.
## int addLayer ( )

Adds an empty layer with default properties to the sprite.
### Return value

Number of the added layer.
## void removeLayer ( int layer )

Removes a given layer from the sprite.
### Arguments

- *int* **layer** - Layer number in range from 1 to the total number of sprite layers.

## void setIntersectionImage ( const Ptr < Image > & image )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to be used as a mask for defining intersections.

## void setIntersectionImageName ( const char * name )

Sets the specified image as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Arguments

- *const char ** **name** - Name of the image to be used as a mask for defining intersections.

## Ptr < Image > getIntersectionImage ( ) const

Returns the image used as a mask for defining intersections with the mouse.
> **Notice:** The image is converted to the R8 format.


### Return value

Image to be used as a mask for defining intersections.
