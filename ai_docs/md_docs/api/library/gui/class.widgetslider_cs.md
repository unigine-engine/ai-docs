# Unigine::WidgetSlider Class (CS)

**Inherits from:** Widget


This class creates a slider: [horizontal](../../../code/gui/ui/ui_widgets.md#hslider) or [vertical](../../../code/gui/ui/ui_widgets.md#vslider) one.


The object of this class may look as follows:


![Horizontal slider](../../../code/gui/ui/widgets/hslider.png)

*Horizontal slider*


![Vertical slider](../../../code/gui/ui/widgets/vslider.png)

*Vertical slider*


#### See Also


- C++ sample
- C# Component sample


## WidgetSlider Class

### Properties

## int Value

The value (position) of the slider.
## int MaxExpand

The maximum value, up to which the upper limit of the range of the slider values can be expanded. The upper limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
## int MinExpand

The minimum value, up to which the lower limit of the range of the slider values can be expanded. The lower limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
## int MaxValue

The maximum value of the slider.
## int MinValue

The minimum value of the slider.
## int ButtonHeight

The height of the slider handle, in pixels (for a vertical slider).
## int ButtonWidth

The width of the slider handle, in pixels (for a horizontal slider).
## int Orientation

The orientation of the slider: horizontal or vertical.
## vec4 ButtonColor

The color of the slider handle.
## vec4 BackgroundColor

The background color of the slider.
### Members

---

## WidgetSlider ( Gui gui , int min = 0 , int max = 100 , int value = 0 )

Constructor. Creates a slider with given properties (horizontal one by default) and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the slider will belong.
- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.

## WidgetSlider ( int min = 0 , int max = 100 , int value = 0 )

Constructor. Creates a slider with given properties (horizontal one by default) and adds it to the Engine GUI.
### Arguments

- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
