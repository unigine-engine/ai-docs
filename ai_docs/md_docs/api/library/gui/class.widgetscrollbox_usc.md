# Unigine::WidgetScrollBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [scroll box](../../../code/gui/ui/ui_containers.md#scrollbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/scrollbox.png)


### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetScrollBox Class

### Members

---

## static WidgetScrollBox ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetScrollBox ( int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setBorder ( int border )

Sets a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Arguments

- *int* **border** - Positive number to enable a border, 0 to disable it.

## int getBorder ( )

Returns a flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Return value

Positive number if a border is enabled; otherwise, 0.
## void setHScrollEnabled ( int enabled )

Sets a value indicating if horizontal scrolling is enabled.
### Arguments

- *int* **enabled** - Positive number to enable horizontal scrolling, 0 to disable it.

## int isHScrollEnabled ( )

Returns a value indicating if horizontal scrolling is enabled.
### Return value

Positive number if scrolling is enabled; otherwise, 0.
## int getHScrollFrameSize ( )

Returns the width of the currently visible area.
### Return value

Width of the visible area in pixels.
## void setHScrollHidden ( int hidden )

Sets a flag indicating if a horizontal scroll bar is hidden, disabled or always rendered.
### Arguments

- *int* **hidden** - Hide flag, one of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.

## int getHScrollHidden ( )

Returns a flag indicating if a horizontal scroll bar is hidden, disabled or always rendered.
### Return value

Hide flag:
- 0 if a scroll bar is always rendered.
- 1 if a scroll bar is automatically hidden when necessary. For example, if the container area is big enough to show all elements, the scroll bar is not rendered. And vice versa, if not all elements can be shown at once, a scroll bar is rendered.
- 2 if a scroll bar is always hidden. In this mode, scroll bar bounds, though a bar itself is not rendered, are still taken into account when the widget bounds are calculated.
- 3 if a scroll bar is always hidden and its size is not added to widget bounds.


## int getHScrollObjectSize ( )

Returns the width of the whole object that should be scrolled.
### Return value

Width of the object being scrolled in pixels.
## int getHScrollStepSize ( )

Returns the step of the horizontal scroller. This step is used to increment the scroll position.
### Return value

Step of the horizontal scroller in pixels.
## void setHScrollValue ( int value )

Sets a position (and also the size) of the horizontal scroller. That is, it sets the width of the currently invisible area that determines the size of the slider.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.

## int getHScrollValue ( )

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
## int getScrollScale ( )

Returns the divisor used to convert integer values into floating point values.
### Return value

Divisor used to scale integers.
## void setSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is specified, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is specified, 0 will be used instead.

## int getSpaceX ( )

Returns the horizontal space between the widgets in the box and between them and the box border.
### Return value

Horizontal space.
## int getSpaceY ( )

Returns the vertical space between the widgets in the box and between them and the box border.
### Return value

Vertical space.
## void setVScrollEnabled ( int enabled )

Sets a value indicating if vertical scrolling is enabled.
### Arguments

- *int* **enabled** - Positive number to enable vertical scrolling, 0 to disable it.

## int isVScrollEnabled ( )

Returns a value indicating if vertical scrolling is enabled.
### Return value

Positive number if scrolling is enabled; otherwise, 0.
## int getVScrollFrameSize ( )

Returns the height of the currently visible area.
### Return value

Height of the visible area in pixels.
## void setVScrollHidden ( int hidden )

Sets a flag indicating if a vertical scroll bar is hidden, disabled or always rendered.
### Arguments

- *int* **hidden** - Hide flag:

  - 0 if a scroll bar is always rendered.
  - 1 if a scroll bar is automatically hidden when necessary. For example, if the container area is big enough to show all elements, the scroll bar is not rendered. And vice versa, if not all elements can be shown at once, a scroll bar is rendered.
  - 2 if a scroll bar is always hidden. In this mode, scroll bar bounds, though a bar itself is not rendered, are still taken into account when the widget bounds are calculated.
  - 3 if a scroll bar is always hidden and its size is not added to widget bounds.

## int getVScrollHidden ( )

Returns a flag indicating if a vertical scroll bar is hidden, disabled or always rendered.
### Return value

Hide flag:
- 0 if a scroll bar is always rendered.
- 1 if a scroll bar is automatically hidden when necessary. For example, if the container area is big enough to show all elements, the scroll bar is not rendered. And vice versa, if not all elements can be shown at once, a scroll bar is rendered.
- 2 if a scroll bar is always hidden. In this mode, scroll bar bounds, though a bar itself is not rendered, are still taken into account when the widget bounds are calculated.
- 3 if a scroll bar is always hidden and its size is not added to widget bounds.


## int getVScrollObjectSize ( )

Returns the height of the whole object that should be scrolled.
### Return value

Height of the object being scrolled in pixels.
## int getVScrollStepSize ( )

Returns the step of the vertical scroller. This step is used to increment the scroll position.
### Return value

Step of the vertical scroller in pixels.
## void setVScrollValue ( int value )

Sets the position (and also the size) of the vertical scroller. That is, it sets the height of the currently invisible area that determines the size of the slider.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object height and the frame height.

## int getVScrollValue ( )

Returns the current position (and also the size) of the vertical scroller. That is, it returns the height of the currently invisible area that determines the size of the slider.
### Return value

Position of the vertical scroller.
## void setBorderColor ( vec4 color )

Sets the border color for the widget.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getBorderColor ( )

Returns the current border color for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( vec4 color )

Sets the background color to be used for the widget.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getBackgroundColor ( )

Returns the current background color used for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setHscrollColor ( vec4 color )

Sets the color to be used for the widget's horizontal scroll.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getHscrollColor ( )

Returns the current color used for the widget's horizontal scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setVscrollColor ( vec4 color )

Sets the color to be used for the widget's vertical scroll.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getVscrollColor ( )

Returns the current color used for the widget's vertical scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBackground ( int background )

Sets a value indicating if a background should be rendered.
### Arguments

- *int* **background** - 1 to render a background, 0 not to render.

## int getBackground ( )

Returns a value indicating if the background is rendered.
### Return value

1 if the background is rendered, 0 if not.
## WidgetScroll getVScroll ( )

Returns the vetical scroller object.
### Return value

Vetical scroller.
## WidgetScroll getHScroll ( )

Returns the horizontal scroller object.
### Return value

Horizontal scroller.
