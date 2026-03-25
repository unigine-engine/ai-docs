# Unigine::WidgetGroupBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [group box](../../../code/gui/ui/ui_containers.md#groupbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/groupbox.png)


## WidgetGroupBox Class

### Members

---

## static WidgetGroupBoxPtr create ( const Ptr < Gui > & gui , const char * str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new box will belong.
- *const char ** **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetGroupBoxPtr create ( const char * str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setBackground ( int background )

Sets a value indicating if a background texture should be rendered for the box.
### Arguments

- *int* **background** - 1 to render a background texture, 0 not to render.

## int getBackground ( ) const

Returns a value indicating if a background texture is rendered for the box.
### Return value

Returns 1 if a background texture is rendered; otherwise, 0.
## void setBorder ( int border )

Sets a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Arguments

- *int* **border** - Positive number to enable a border, 0 to disable it.

## int getBorder ( ) const

Returns a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Return value

Positive number if a border is enabled; otherwise, 0.
## void setColor ( const Math:: vec4 & color )

Sets a color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to set.

## Math:: vec4 getColor ( ) const

Returns a color of the global color multiplier.
### Return value

Color of the color multiplier.
## void setPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## int getPaddingBottom ( ) const

Returns the current bottom padding for the widget content.
### Return value

Bottom padding in pixels.
## int getPaddingLeft ( ) const

Returns the current left-side padding for the widget content.
### Return value

Left-side padding in pixels.
## int getPaddingRight ( ) const

Returns the current right-side padding for the widget content.
### Return value

Right-side padding in pixels.
## int getPaddingTop ( ) const

Returns the current top padding for the widget content.
### Return value

Top padding in pixels.
## void setSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is specified, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is specified, 0 will be used instead.

## int getSpaceX ( ) const

Returns the horizontal space between the widgets in the box and between them and the box border.
### Return value

Horizontal space.
## int getSpaceY ( ) const

Returns the vertical space between the widgets in the box and between them and the box border.
### Return value

Vertical space.
## void setStencil ( int stencil )

Sets a value indicating if a widget cuts off its children along its bounds. Everything that lies outside of them, is not rendered. The default is 0.
### Arguments

- *int* **stencil** - 1 to enable cutting; otherwise, 0.

## int getStencil ( ) const

Returns a value indicating if a widget cuts off its children along its set bounds. Everything that lies outside of them, is not rendered. This option works only if children have ALIGN_OVERLAP flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Return value

Returns 1 if cutting is enabled; otherwise, 0.
## void setText ( const char * text )

Sets a box title.
### Arguments

- *const char ** **text** - Box title.

## const char * getText ( ) const

Returns the box title.
### Return value

Box title.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets the background color to be used for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBackgroundColor ( ) const

Returns the current background color used for the widget.
### Return value

The four-component vector specifying the color in the RGBA format.
## void setBorderColor ( const Math:: vec4 & color )

Sets the border color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBorderColor ( ) const

Returns the current border color for the widget.
### Return value

The four-component vector specifying the color in the RGBA format.
