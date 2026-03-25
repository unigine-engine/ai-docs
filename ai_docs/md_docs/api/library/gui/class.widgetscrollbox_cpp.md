# Unigine::WidgetScrollBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [scroll box](../../../code/gui/ui/ui_containers.md#scrollbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/scrollbox.png)


### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetScrollBox Class

### Enums

## SCROLL_RENDER_MODE

| Name | Description |
|---|---|
| **ALWAYS_RENDER** = 0 | Scroll bar is always rendered. |
| **AUTO_HIDE** = 1 | Scroll bar is automatically hidden when necessary. For example, if the container area is big enough to show all elements, the scroll bar is not rendered. And vice versa, if not all elements can be shown at once, a scroll bar is rendered. |
| **ALWAYS_HIDE** = 2 | Scroll bar is always hidden. In this mode, though a bar itself is not rendered, the scroll bar bounds are still taken into account when the widget bounds are calculated. |
| **ALWAYS_HIDE_NO_BOUNDS** = 3 | Scroll bar is always hidden and its size is not added to widget bounds. |

### Members

---

## static WidgetScrollBoxPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetScrollBoxPtr create ( int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setBorder ( int border )

Sets a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Arguments

- *int* **border** - Positive number to enable a border, 0 to disable it.

## int getBorder ( ) const

Returns a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Return value

Positive number if a border is enabled; otherwise, 0.
## void setHScrollEnabled ( bool enabled )

Sets a value indicating if horizontal scrolling is enabled.
### Arguments

- *bool* **enabled** - Positive number to enable horizontal scrolling, 0 to disable it.

## bool isHScrollEnabled ( ) const

Returns a value indicating if horizontal scrolling is enabled.
### Return value

Positive number if scrolling is enabled; otherwise, 0.
## int getHScrollFrameSize ( ) const

Returns the width of the currently visible area.
### Return value

Width of the visible area in pixels.
## void setHScrollHidden ( WidgetScrollBox::SCROLL_RENDER_MODE hidden )

Sets a flag indicating if a horizontal scroll bar is hidden, disabled or always rendered.
### Arguments

- *[WidgetScrollBox::SCROLL_RENDER_MODE](../../../api/library/gui/class.widgetscrollbox_cpp.md#SCROLL_RENDER_MODE)* **hidden** - Hide flag, one of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.

## WidgetScrollBox::SCROLL_RENDER_MODE getHScrollHidden ( ) const

Returns a flag indicating if a horizontal scroll bar is hidden, disabled or always rendered.
### Return value

Hide flag, one of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
## int getHScrollObjectSize ( ) const

Returns the width of the whole object that should be scrolled.
### Return value

Width of the object being scrolled in pixels.
## int getHScrollStepSize ( ) const

Returns the step of the horizontal scroller. This step is used to increment the scroll position.
### Return value

Step of the horizontal scroller in pixels.
## void setHScrollValue ( int value )

Sets a position (and also the size) of the horizontal scroller. That is, it sets the width of the currently invisible area that determines the size of the slider.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.

## int getHScrollValue ( ) const

Returns the current position (and also automatically the size) of the horizontal scroller. That is, it returns the width of the currently invisible area that determines the size of the slider.
### Return value

Position of the horizontal scroller.
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
## int getScrollScale ( ) const

Returns the divisor used to convert integer values into floating point values.
### Return value

Divisor used to scale integers.
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
## void setVScrollEnabled ( bool enabled )

Sets a value indicating if vertical scrolling is enabled.
### Arguments

- *bool* **enabled** - Positive number to enable vertical scrolling, 0 to disable it.

## bool isVScrollEnabled ( ) const

Returns a value indicating if vertical scrolling is enabled.
### Return value

Positive number if scrolling is enabled; otherwise, 0.
## int getVScrollFrameSize ( ) const

Returns the height of the currently visible area.
### Return value

Height of the visible area in pixels.
## void setVScrollHidden ( WidgetScrollBox::SCROLL_RENDER_MODE hidden )

Sets a flag indicating if a vertical scroll bar is hidden, disabled or always rendered.
### Arguments

- *[WidgetScrollBox::SCROLL_RENDER_MODE](../../../api/library/gui/class.widgetscrollbox_cpp.md#SCROLL_RENDER_MODE)* **hidden** - Hide flag, one of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.

## WidgetScrollBox::SCROLL_RENDER_MODE getVScrollHidden ( ) const

Returns a flag indicating if a vertical scroll bar is hidden, disabled or always rendered.
### Return value

Hide flag, one of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
## int getVScrollObjectSize ( ) const

Returns the height of the whole object that should be scrolled.
### Return value

Height of the object being scrolled in pixels.
## int getVScrollStepSize ( ) const

Returns the step of the vertical scroller. This step is used to increment the scroll position.
### Return value

Step of the vertical scroller in pixels.
## void setVScrollValue ( int value )

Sets the position (and also the size) of the vertical scroller. That is, it sets the height of the currently invisible area that determines the size of the slider.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object height and the frame height.

## int getVScrollValue ( ) const

Returns the current position (and also the size) of the vertical scroller. That is, it returns the height of the currently invisible area that determines the size of the slider.
### Return value

Position of the vertical scroller.
## void setBorderColor ( const Math:: vec4 & color )

Sets the border color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBorderColor ( ) const

Returns the current border color for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets the background color to be used for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBackgroundColor ( ) const

Returns the current background color used for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setHscrollColor ( const Math:: vec4 & color )

Sets the color to be used for the widget's horizontal scroll.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getHscrollColor ( ) const

Returns the current color used for the widget's horizontal scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setVscrollColor ( const Math:: vec4 & color )

Sets the color to be used for the widget's vertical scroll.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getVscrollColor ( ) const

Returns the current color used for the widget's vertical scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBackground ( int background )

Sets a value indicating if a background should be rendered.
### Arguments

- *int* **background** - 1 to render a background, 0 not to render.

## int getBackground ( ) const

Returns a value indicating if the background is rendered.
### Return value

1 if the background is rendered, 0 if not.
## Ptr < WidgetScroll > getVScroll ( ) const

Returns the vetical scroller object.
### Return value

Vetical scroller.
## Ptr < WidgetScroll > getHScroll ( ) const

Returns the horizontal scroller object.
### Return value

Horizontal scroller.
