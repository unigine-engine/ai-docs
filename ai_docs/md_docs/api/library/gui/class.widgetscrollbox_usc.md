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

## WidgetScroll getHScroll () const

Returns the current horizontal scroller object.
### Return value

Current horizontal scroller object
## void setHScrollValue ( int value )

Sets a new position (and also automatically the size) of the horizontal scroller. That is, it returns the width of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object width and the frame width.
### Arguments

- *int* **value** - The position (and also automatically the size) of the horizontal scroller

## int getHScrollValue () const

Returns the current position (and also automatically the size) of the horizontal scroller. That is, it returns the width of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object width and the frame width.
### Return value

Current position (and also automatically the size) of the horizontal scroller
## int getHScrollStepSize () const

Returns the current step of the horizontal scroller. This step is used to increment the scroll position.
### Return value

Current step of the horizontal scroller
## int getHScrollFrameSize () const

Returns the current width of the currently visible area.
### Return value

Current width of the currently visible area
## int getHScrollObjectSize () const

Returns the current width of the whole object that should be scrolled.
### Return value

Current width of the whole object that should be scrolled
## void setHScrollHidden ( int hidden )

Sets a new flag indicating if a horizontal scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
### Arguments

- *int* **hidden** - The flag indicating if a horizontal scroll bar is hidden, disabled or always rendered

## int getHScrollHidden () const

Returns the current flag indicating if a horizontal scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
### Return value

Current flag indicating if a horizontal scroll bar is hidden, disabled or always rendered
## void setHScrollEnabled ( int enabled )

Sets a new value indicating if horizontal scrolling is enabled.
### Arguments

- *int* **enabled** - The horizontal scrolling

## int isHScrollEnabled () const

Returns the current value indicating if horizontal scrolling is enabled.
### Return value

Current horizontal scrolling
## WidgetScroll getVScroll () const

Returns the current vertical scroller object.
### Return value

Current vertical scroller object
## void setVScrollValue ( int value )

Sets a new position (and also the size) of the vertical scroller. That is, it returns the height of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object height and the frame height.
### Arguments

- *int* **value** - The position (and also the size) of the vertical scroller

## int getVScrollValue () const

Returns the current position (and also the size) of the vertical scroller. That is, it returns the height of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object height and the frame height.
### Return value

Current position (and also the size) of the vertical scroller
## int getVScrollStepSize () const

Returns the current step of the vertical scroller. This step is used to increment the scroll position.
### Return value

Current step of the vertical scroller
## int getVScrollFrameSize () const

Returns the current height of the currently visible area.
### Return value

Current height of the currently visible area
## int getVScrollObjectSize () const

Returns the current height of the whole object that should be scrolled.
### Return value

Current height of the whole object that should be scrolled
## void setVScrollHidden ( int hidden )

Sets a new flag indicating if a vertical scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
### Arguments

- *int* **hidden** - The flag indicating if a vertical scroll bar is hidden, disabled or always rendered

## int getVScrollHidden () const

Returns the current flag indicating if a vertical scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
### Return value

Current flag indicating if a vertical scroll bar is hidden, disabled or always rendered
## void setVScrollEnabled ( int enabled )

Sets a new value indicating if vertical scrolling is enabled.
### Arguments

- *int* **enabled** - The vertical scrolling

## int isVScrollEnabled () const

Returns the current value indicating if vertical scrolling is enabled.
### Return value

Current vertical scrolling
## int getScrollScale () const

Returns the current divisor used to convert integer values into floating point values.
### Return value

Current divisor used to convert integer values into floating point values
## void setBackground ( int background )

Sets a new value indicating if the background is rendered.
### Arguments

- *int* **background** - The value indicating if the background is rendered

## int getBackground () const

Returns the current value indicating if the background is rendered.
### Return value

Current value indicating if the background is rendered
## void setBorder ( int border )

Sets a new flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Arguments

- *int* **border** - The flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box)

## int getBorder () const

Returns the current flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
### Return value

Current flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box)
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
## void setVscrollColor ( vec4 color )

Sets a new color used for the widget's vertical scroll.
### Arguments

- *vec4* **color** - The color used for the widget's vertical scroll

## vec4 getVscrollColor () const

Returns the current color used for the widget's vertical scroll.
### Return value

Current color used for the widget's vertical scroll
## void setHscrollColor ( vec4 color )

Sets a new color used for the widget's horizontal scroll.
### Arguments

- *vec4* **color** - The color used for the widget's horizontal scroll

## vec4 getHscrollColor () const

Returns the current color used for the widget's horizontal scroll.
### Return value

Current color used for the widget's horizontal scroll
## void setBackgroundColor ( vec4 color )

Sets a new background color used for the widget.
### Arguments

- *vec4* **color** - The background color used for the widget

## vec4 getBackgroundColor () const

Returns the current background color used for the widget.
### Return value

Current background color used for the widget
## void setBorderColor ( vec4 color )

Sets a new border color for the widget.
### Arguments

- *vec4* **color** - The border color for the widget

## vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current border color for the widget
## int getSpaceY () const

Returns the current vertical space between the widgets in the box and between them and the box border.
### Return value

Current vertical space between the widgets in the box and between them and the box border
## int getSpaceX () const

Returns the current horizontal space between the widgets in the box and between them and the box border.
### Return value

Current horizontal space between the widgets in the box and between them and the box border
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
