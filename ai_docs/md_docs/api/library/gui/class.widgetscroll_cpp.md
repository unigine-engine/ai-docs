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

## void setFrameSize ( int size )

Sets the size of the currently visible area.
### Arguments

- *int* **size** - Size of the visible area in pixels. The minimum is 1 pixel.

## int getFrameSize ( ) const

Returns the size of the currently visible area.
### Return value

Size of the visible area in pixels.
## void setObjectSize ( int size )

Sets the size of the whole area to be scrolled through.
### Arguments

- *int* **size** - Size of the object being scrolled in pixels. The minimum is 1 pixel.

## int getObjectSize ( ) const

Returns the size of the whole area that is scrolled through.
### Return value

Size of the object being scrolled in pixels.
## void setOrientation ( int orientation )

Sets orientation of the scroller: horizontal (by default) or vertical one.
### Arguments

- *int* **orientation** - 1 to set horizontal orientation; 0 to set vertical one.

## int getOrientation ( ) const

Returns the current orientation of the scroller: horizontal or vertical one.
### Return value

1 if the orientation is horizontal; 0 if it is vertical.
## void setStepSize ( int size )

Sets the step of the scroller. This step is used to increment the scroll position.
### Arguments

- *int* **size** - Step of the scroller in pixels. The minimum is 1 pixel.

## int getStepSize ( ) const

Returns the step of the scroller. This step is used to increment the scroll position.
### Return value

Step of the scroller in pixels.
## void setValue ( int value )

Sets a value of the scroller, i.e. its position.
### Arguments

- *int* **value** - Position of the scroller. The minimum value is 0, the maximum value is the difference between the object width and the frame width.

## int getValue ( ) const

Returns the value of the scroller, i.e. its position.
### Return value

Position of the scroller.
## void setScrollColor ( const Math:: vec4 & color )

Sets the color to be used for the widget's scroll.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getScrollColor ( ) const

Returns the current color used for the widget's scroll.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setSliderButton ( bool button )

Sets the display of slider buttons.
### Arguments

- *bool* **button** - true to display slider buttons, otherwise, false.

## bool isSliderButton ( ) const

Returns a value indicating if slider buttons are displayed.
### Return value

true if slider buttons are displayed, otherwise, false.
## void setMouseWheelOrientation ( int orientation )

Sets orientation of the mouse wheel scroll: horizontal or vertical (by default).
### Arguments

- *int* **orientation** - 1 to set horizontal orientation; 0 to set vertical one.

## int getMouseWheelOrientation ( ) const

Returns orientation of the mouse wheel scroll: horizontal or vertical.
### Return value

1 if the orientation is horizontal; 0 if it is vertical.
