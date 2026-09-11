# Unigine::WidgetScroll Class (CPP)

**Header:** #include <UnigineWidgets.h>

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

## void setSliderButton ( bool button )

Sets a new value indicating if slider buttons are displayed.
### Arguments

- *bool* **button** - Set **true** to enable display of the slider buttons; **false** - to disable it.

## bool isSliderButton () const

Returns the current value indicating if slider buttons are displayed.
### Return value

**true** if display of the slider buttons is enabled ; otherwise **false**.
## void setValue ( int value )

Sets a new value (position) of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.
### Arguments

- *int* **value** - The value (position) of the scroller

## int getValue () const

Returns the current value (position) of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.
### Return value

Current value (position) of the scroller
## void setStepSize ( int size )

Sets a new step of the scroller. This step is used to increment the scroll position.
### Arguments

- *int* **size** - The step used to increment the scroll position

## int getStepSize () const

Returns the current step of the scroller. This step is used to increment the scroll position.
### Return value

Current step used to increment the scroll position
## void setFrameSize ( int size )

Sets a new size of the visible area, in pixels. The minimum is 1 pixel.
### Arguments

- *int* **size** - The size of the visible area

## int getFrameSize () const

Returns the current size of the visible area, in pixels. The minimum is 1 pixel.
### Return value

Current size of the visible area
## void setObjectSize ( int size )

Sets a new size of the whole area that is scrolled through.
### Arguments

- *int* **size** - The size of the whole area that is scrolled through

## int getObjectSize () const

Returns the current size of the whole area that is scrolled through.
### Return value

Current size of the whole area that is scrolled through
## void setOrientation ( int orientation )

Sets a new orientation of the scroller: horizontal or vertical.
### Arguments

- *int* **orientation** - The orientation of the scroller (horizontal or vertical)

## int getOrientation () const

Returns the current orientation of the scroller: horizontal or vertical.
### Return value

Current orientation of the scroller (horizontal or vertical)
## void setScrollColor ( const Math:: vec4 & color )

Sets a new color used for the widget's scroll.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color used for the widget's scroll

## Math:: vec4 getScrollColor () const

Returns the current color used for the widget's scroll.
### Return value

Current color used for the widget's scroll
## void setMouseWheelOrientation ( int orientation )

Sets a new orientation of the mouse wheel scroll: horizontal or vertical.
### Arguments

- *int* **orientation** - The orientation of the mouse wheel scroll (horizontal or vertical)

## int getMouseWheelOrientation () const

Returns the current orientation of the mouse wheel scroll: horizontal or vertical.
### Return value

Current orientation of the mouse wheel scroll (horizontal or vertical)
---

## static WidgetScrollPtr create ( const Ptr < Gui > & gui , int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the scroll bar will belong.
- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.

## static WidgetScrollPtr create ( int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the Engine GUI.
### Arguments

- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.
