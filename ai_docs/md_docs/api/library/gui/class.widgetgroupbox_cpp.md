# Unigine::WidgetGroupBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [group box](../../../code/gui/ui/ui_containers.md#groupbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/groupbox.png)


## WidgetGroupBox Class

### Members

## void setText ( const char * text )

Sets a new box title.
### Arguments

- *const char ** **text** - The box title

## const char * getText () const

Returns the current box title.
### Return value

Current box title
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the box.
### Arguments

- *int* **background** - The flag indicating whether a background texture is rendered for the box

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the box.
### Return value

Current flag indicating whether a background texture is rendered for the box
## void setColor ( const Math:: vec4 & color )

Sets a new color of the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the global color multiplier

## Math:: vec4 getColor () const

Returns the current color of the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Return value

Current color of the global color multiplier
## void setStencil ( int stencil )

Sets a new value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cpp.md#setWidth_int_void). Everything that lies outside of them is not rendered. This option works only if children have the *[ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP)* flag set (otherwise, they will expand the box widget bounds and no cutting will be done). The default is 0.
### Arguments

- *int* **stencil** - The flag indicating whether the widget cuts off its children along its set bounds

## int getStencil () const

Returns the current value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cpp.md#setWidth_int_void). Everything that lies outside of them is not rendered. This option works only if children have the *[ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP)* flag set (otherwise, they will expand the box widget bounds and no cutting will be done). The default is 0.
### Return value

Current flag indicating whether the widget cuts off its children along its set bounds
## void setBorder ( int border )

Sets a new flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Arguments

- *int* **border** - The flag indicating whether a one-pixel border is rendered around the widget content

## int getBorder () const

Returns the current flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Return value

Current flag indicating whether a one-pixel border is rendered around the widget content
## int getPaddingBottom () const

Returns the current bottom padding for the widget content.
### Return value

Current bottom padding for the widget content
## int getPaddingTop () const

Returns the current top padding for the widget content.
### Return value

Current top padding for the widget content
## int getPaddingRight () const

Returns the current right-side padding for the widget content.
### Return value

Current right-side padding for the widget content
## int getPaddingLeft () const

Returns the current left-side padding for the widget content.
### Return value

Current left-side padding for the widget content
## int getSpaceY () const

Returns the current vertical space between the widgets in the box and between them and the box border.
### Return value

Current vertical space between the widgets in the box and between them and the box border
## int getSpaceX () const

Returns the current horizontal space between the widgets in the box and between them and the box border.
### Return value

Current horizontal space between the widgets in the box and between them and the box border
## void setBorderColor ( const Math:: vec4 & color )

Sets a new border color of the box.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The border color of the box

## Math:: vec4 getBorderColor () const

Returns the current border color of the box.
### Return value

Current border color of the box
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color of the box.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The background color of the box

## Math:: vec4 getBackgroundColor () const

Returns the current background color of the box.
### Return value

Current background color of the box
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
