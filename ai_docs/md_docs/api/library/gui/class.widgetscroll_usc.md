# Unigine::WidgetScroll Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a scrollbar: [horizontal](../../../code/gui/ui/ui_widgets.md#hscroll) or [vertical](../../../code/gui/ui/ui_widgets.md#vscroll) one.


The object of this class may look as follows:


![Horizontal scroll](../../../code/gui/ui/widgets/hscroll.png)

*Horizontal scroll*


![Vertical scroll](../../../code/gui/ui/widgets/vscroll.png)

*Vertical scroll*


#### See Also


- C++ sample
- C# Component sample


## WidgetScroll Class

### Members

---

## static WidgetScroll ( Gui gui , int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the scroll bar will belong.
- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.

## static WidgetScroll ( int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the Engine GUI.
### Arguments

- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.

## void setFrameSize ( int size )

Sets the size of the currently visible area.
### Arguments

- *int* **size** - Size of the visible area in pixels. The minimum is 1 pixel.

## int getFrameSize ( )

Returns the size of the currently visible area.
### Return value

Size of the visible area in pixels.
## void setObjectSize ( int size )

Sets the size of the whole area to be scrolled through.
### Arguments

- *int* **size** - Size of the object being scrolled in pixels. The minimum is 1 pixel.

## int getObjectSize ( )

Returns the size of the whole area that is scrolled through.
### Return value

Size of the object being scrolled in pixels.
## void setOrientation ( int orientation )

Sets orientation of the scroller: horizontal (by default) or vertical one.
### Arguments

- *int* **orientation** - 1 to set horizontal orientation; 0 to set vertical one.

## int getOrientation ( )

Returns the current orientation of the scroller: horizontal or vertical one.
### Return value

1 if the orientation is horizontal; 0 if it is vertical.
## void setStepSize ( int size )

Sets the step of the scroller. This step is used to increment the scroll position.
### Arguments

- *int* **size** - Step of the scroller in pixels. The minimum is 1 pixel.

## int getStepSize ( )

Returns the step of the scroller. This step is used to increment the scroll position.
### Return value

Step of the scroller in pixels.
## void setValue ( int value )

Sets a value of the scroller, i.e. its position.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.

## int getValue ( )

Returns the value of the scroller, i.e. its position.
### Return value

Position of the scroller.
## void setScrollColor ( vec4 color )

Sets the color to be used for the widget's scroll.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getScrollColor ( )

Returns the current color used for the widget's scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setSliderButton ( int button )

Sets the display of slider buttons.
### Arguments

- *int* **button** - **1** to display slider buttons, otherwise, **0**.

## int isSliderButton ( )

Returns a value indicating if slider buttons are displayed.
### Return value

**1** if slider buttons are displayed, otherwise, **0**.
## void setMouseWheelOrientation ( int orientation )

Sets orientation of the mouse wheel scroll: horizontal or vertical (by default).
### Arguments

- *int* **orientation** - 1 to set horizontal orientation; 0 to set vertical one.

## int getMouseWheelOrientation ( )

Returns orientation of the mouse wheel scroll: horizontal or vertical.
### Return value

1 if the orientation is horizontal; 0 if it is vertical.
