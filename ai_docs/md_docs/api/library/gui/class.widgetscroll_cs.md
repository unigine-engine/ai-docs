# Unigine::WidgetScroll Class (CS)

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

### Properties

## bool SliderButton

The value indicating if slider buttons are displayed.
## int Value

The value of the scroller, i.e. its position.
## int StepSize

The step of the scroller. This step is used to increment the scroll position.
## int FrameSize

The size of the currently visible area.
## int ObjectSize

The size of the whole area that is scrolled through.
## int Orientation

The orientation of the scroller: horizontal or vertical one.
## vec4 ScrollColor

The color used for the widget's scroll.
## int MouseWheelOrientation

The 1 if the orientation is horizontal; 0 if it is vertical.
### Members

---

## WidgetScroll ( Gui gui , int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the scroll bar will belong.
- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.

## WidgetScroll ( int object = 100 , int frame = 10 , int step = 1 , int value = 0 )

Constructor. Creates a scroller with the given parameters and adds it to the Engine GUI.
### Arguments

- *int* **object** - Width of the object to scroll in pixels. This is an optional argument.
- *int* **frame** - Width of the visible area in pixels. This is an optional argument.
- *int* **step** - Step of the scroller in pixels. This is an optional argument.
- *int* **value** - Initial position of the scroller. This is an optional argument.
