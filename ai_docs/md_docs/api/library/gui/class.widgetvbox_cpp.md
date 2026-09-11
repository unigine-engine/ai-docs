# Unigine::WidgetVBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [single vertical column](../../../code/gui/ui/ui_containers.md#vbox) container.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/vbox.png)


## WidgetVBox Class

### Members

## void setBorder ( bool border )

Sets a new value indicating if the border is displayed.
### Arguments

- *bool* **border** - Set **true** to enable display of the border; **false** - to disable it.

## bool isBorder () const

Returns the current value indicating if the border is displayed.
### Return value

**true** if display of the border is enabled ; otherwise **false**.
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the box.
### Arguments

- *int* **background** - The value indicating if a background texture is rendered for the box

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the box.
### Return value

Current value indicating if a background texture is rendered for the box
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color used for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBackgroundColor () const

Returns the current background color used for the widget.
### Return value

Current Four-component vector specifying the color in the RGBA format.
## void setColor ( const Math:: vec4 & color )

Sets a new color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The Multiplier color.

## Math:: vec4 getColor () const

Returns the current color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Return value

Current Multiplier color.
## void setStencil ( int stencil )

Sets a new value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cpp.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Arguments

- *int* **stencil** - The value indicating if a widget cuts off its children along its set bounds

## int getStencil () const

Returns the current value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cpp.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Return value

Current value indicating if a widget cuts off its children along its set bounds
## int getPaddingBottom () const

Returns the current bottom padding for the widget content.
### Return value

Current bottom padding in pixels.
## int getPaddingTop () const

Returns the current top padding for the widget content.
### Return value

Current top padding in pixels.
## int getPaddingRight () const

Returns the current right-side padding for the widget content.
### Return value

Current right-side padding in pixels.
## int getPaddingLeft () const

Returns the current left-side padding for the widget content.
### Return value

Current left-side padding in pixels.
## int getSpaceY () const

Returns the current vertical space between the widgets in the box and between them and the box border.
### Return value

Current vertical space.
## int getSpaceX () const

Returns the current horizontal space between the widgets in the box and between them and the box border.
### Return value

Current horizontal space.
## void setBackgroundCustomFilter ( int filter )

Sets a new custom [filtering mode](../../../api/library/rendering/class.texture_cpp.md) for the texture used as the background of the widget.
### Arguments

- *int* **filter** - The [texture flag](../../../api/library/rendering/class.texture_cpp.md#sampler_flags).

## int getBackgroundCustomFilter () const

Returns the current custom [filtering mode](../../../api/library/rendering/class.texture_cpp.md) for the texture used as the background of the widget.
### Return value

Current [texture flag](../../../api/library/rendering/class.texture_cpp.md#sampler_flags).
## void setBackgroundCustomFilterEnabled ( bool enabled )

Sets a new value indicating whether a custom filtering mode for the background texture is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable a custom filtering mode for the background texture; **false** - to disable it.

## bool isBackgroundCustomFilterEnabled () const

Returns the current value indicating whether a custom filtering mode for the background texture is enabled.
### Return value

**true** if a custom filtering mode for the background texture is enabled ; otherwise **false**.
## void setBackground9SliceScale ( float scale )

Sets a new value that controls scaling for corners of a background texture when 9-sliced mode is enabled.
### Arguments

- *float* **scale** - The value to control scaling for corners of the background texture; the default is 1.

## float getBackground9SliceScale () const

Returns the current value that controls scaling for corners of a background texture when 9-sliced mode is enabled.
### Return value

Current value to control scaling for corners of the background texture; the default is 1.
## void setBackground9Sliced ( bool sliced )

Sets a new value indicating whether 9-sliced mode is enabled.
### Arguments

- *bool* **sliced** - Set **true** to enable the 9-sliced mode for the widget background; **false** - to disable it.

## bool isBackground9Sliced () const

Returns the current value indicating whether 9-sliced mode is enabled.
### Return value

**true** if the 9-sliced mode for the widget background is enabled ; otherwise **false**.
## void setBackgroundTexture ( const char * texture )

Sets a new texture path for the widget background.
### Arguments

- *const char ** **texture** - The path to the texture.

## const char * getBackgroundTexture () const

Returns the current texture path for the widget background.
### Return value

Current path to the texture.
---

## static WidgetVBoxPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates a vertical box with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetVBoxPtr create ( int x = 0 , int y = 0 )

Constructor. Creates a vertical box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void setSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is specified, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is specified, 0 will be used instead.

## void setBackgroundImage ( const Ptr < Image > & image , int dynamic = 0 )

Sets an image loaded into memory as the background of the widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Pointer to the image.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Ptr < Image > getBackgroundImage ( ) const

Returns a pointer to the image currently set as the background of the widget.
### Return value

Pointer to the image.
## void setBackgroundRender ( const Ptr < Texture > & texture , int flipped = 0 )

Sets a texture to be rendered as the background of the widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Ptr < Texture > getBackgroundRender ( ) const

Returns a pointer to the texture currently set as the background of the widget.
### Return value

Pointer to the texture.
## void setBackground9SliceOffsets ( float l , float r , float t , float b )

Sets the offsets for the background texture when 9-slice mode is enabled. Offsets are specified in normalized values (from 0 to 1).
### Arguments

- *float* **l** - Left-side offset.
- *float* **r** - Right-side offset.
- *float* **t** - Top offset.
- *float* **b** - Bottom offset.

## Math:: vec4 getBackground9SliceOffsets ( ) const

Gets the vector of offset values for the background texture when 9-slice mode is enabled.
### Return value

The vector of offset values.
## void setBackgroundBlendFunc ( int src , int dest )

### Arguments

- *int* **src**
- *int* **dest**

## int getBackgroundBlendSrcFunc ( ) const

## int getBackgroundBlendDestFunc ( ) const
