# Unigine::WidgetVBox Class (CS)

**Inherits from:** Widget


This class creates a [single vertical column](../../../code/gui/ui/ui_containers.md#vbox) container.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/vbox.png)


## WidgetVBox Class

### Properties

## bool Border

The value indicating if the border is displayed.
## int Background

The value indicating if a background texture is rendered for the box.
## vec4 BackgroundColor

The background color used for the widget.
## vec4 Color

The color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
## int Stencil

The value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cs.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_cs.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
## 🔒︎ int PaddingBottom

The bottom padding for the widget content.
## 🔒︎ int PaddingTop

The top padding for the widget content.
## 🔒︎ int PaddingRight

The right-side padding for the widget content.
## 🔒︎ int PaddingLeft

The left-side padding for the widget content.
## 🔒︎ int SpaceY

The vertical space between the widgets in the box and between them and the box border.
## 🔒︎ int SpaceX

The horizontal space between the widgets in the box and between them and the box border.
## int BackgroundCustomFilter

The custom [filtering mode](../../../api/library/rendering/class.texture_cs.md) for the texture used as the background of the widget.
## bool BackgroundCustomFilterEnabled

The value indicating whether a custom filtering mode for the background texture is enabled.
## float Background9SliceScale

The value that controls scaling for corners of a background texture when 9-sliced mode is enabled.
## bool Background9Sliced

The value indicating whether 9-sliced mode is enabled.
## string BackgroundTexture

The texture path for the widget background.
### Members

---

## WidgetVBox ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates a vertical box with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## WidgetVBox ( int x = 0 , int y = 0 )

Constructor. Creates a vertical box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void SetPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void SetSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is specified, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is specified, 0 will be used instead.

## void SetBackgroundImage ( Image image , int dynamic = 0 )

Sets an image loaded into memory as the background of the widget.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Pointer to the image.
- *int* **dynamic** - Positive number if the image will be updated each frame; otherwise, 0.

## Image GetBackgroundImage ( )

Returns a pointer to the image currently set as the background of the widget.
### Return value

Pointer to the image.
## void SetBackgroundRender ( Texture texture , int flipped = 0 )

Sets a texture to be rendered as the background of the widget.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Pointer to the texture.
- *int* **flipped** - Flipped flag.

## Texture GetBackgroundRender ( )

Returns a pointer to the texture currently set as the background of the widget.
### Return value

Pointer to the texture.
## void SetBackground9SliceOffsets ( float l , float r , float t , float b )

Sets the offsets for the background texture when 9-slice mode is enabled. Offsets are specified in normalized values (from 0 to 1).
### Arguments

- *float* **l** - Left-side offset.
- *float* **r** - Right-side offset.
- *float* **t** - Top offset.
- *float* **b** - Bottom offset.

## vec4 GetBackground9SliceOffsets ( )

Gets the vector of offset values for the background texture when 9-slice mode is enabled.
### Return value

The vector of offset values.
## void SetBackgroundBlendFunc ( int src , int dest )

### Arguments

- *int* **src**
- *int* **dest**

## int GetBackgroundBlendSrcFunc ( )

## int GetBackgroundBlendDestFunc ( )
