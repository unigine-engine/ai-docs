# Unigine::WidgetGroupBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [group box](../../../code/gui/ui/ui_containers.md#groupbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/groupbox.png)


## WidgetGroupBox Class

### Members

---

## static WidgetGroupBox ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new box will belong.
- *string* **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetGroupBox ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setBackground ( int background )

Sets a value indicating if a background texture should be rendered for the box.
### Arguments

- *int* **background** - 1 to render a background texture, 0 not to render.

## int getBackground ( )

Returns a value indicating if a background texture is rendered for the box.
### Return value

**1** if a background texture is rendered; otherwise, **0**.
## void setBorder ( int border )

Sets a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). By default, the border is always rendered.
### Arguments

- *int* **border** - 1 to use a border around the content; 0 not to use a border.

## int getBorder ( )

Returns a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box).
### Return value

1 if a border is rendered; otherwise, 0.
## void setColor ( vec4 color )

Sets a color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
### Arguments

- *vec4* **color** - Color multiplier.

## vec4 getColor ( )

Returns a color of the global color multiplier.
### Return value

A multiplier color.
## void setPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## int getPaddingBottom ( )

Returns the current bottom padding for the widget content.
### Return value

Bottom padding in pixels.
## int getPaddingLeft ( )

Returns the current left-side padding for the widget content.
### Return value

Left-side padding in pixels.
## int getPaddingRight ( )

Returns the current right-side padding for the widget content.
### Return value

Right-side padding in pixels.
## int getPaddingTop ( )

Returns the current top padding for the widget content.
### Return value

Top padding in pixels.
## void setSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space.
- *int* **y** - Vertical space.

## int getSpaceX ( )

Returns the horizontal space between the widgets in the box and between them and the box border.
### Return value

Horizontal space.
## int getSpaceY ( )

Returns the vertical space between the widgets in the box and between them and the box border.
### Return value

Vertical space.
## void setStencil ( int stencil )

Sets a value indicating if a widget cuts off its children along its [bounds](../../../api/library/gui/class.widget_usc.md#setWidth_int_void). Everything that lies outside of them, is not rendered.
### Arguments

- *int* **stencil** - 1 to enable cutting; otherwise, 0.

## int getStencil ( )

Returns a value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_usc.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [GUI_ALIGN_OVERLAP](../../../api/library/gui/class.gui_usc.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Return value

**1** if cutting is enabled; otherwise, **0**.
## void setText ( string text )

Sets a box title.
### Arguments

- *string* **text** - Box title.

## string getText ( )

Returns the box title.
### Return value

Box title.
## void setBackgroundColor ( vec4 color )

Sets the background color to be used for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBackgroundColor ( )

Returns the current background color used for the widget.
### Return value

The four-component vector specifying the color in the RGBA format.
## void setBorderColor ( vec4 color )

Sets the border color for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBorderColor ( )

Returns the current border color for the widget.
### Return value

The four-component vector specifying the color in the RGBA format.
