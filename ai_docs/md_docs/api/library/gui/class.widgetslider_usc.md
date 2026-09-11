# Unigine::WidgetSlider Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

### Members

## void setValue ( int value )

Sets a new value (position) of the slider.
### Arguments

- *int* **value** - The value (position) of the slider

## int getValue () const

Returns the current value (position) of the slider.
### Return value

Current value (position) of the slider
## void setMaxExpand ( int expand )

Sets a new maximum value, up to which the upper limit of the range of the slider values can be expanded. The upper limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Arguments

- *int* **expand** - The maximum value, up to which the upper limit of the slider value range can be expanded

## int getMaxExpand () const

Returns the current maximum value, up to which the upper limit of the range of the slider values can be expanded. The upper limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Return value

Current maximum value, up to which the upper limit of the slider value range can be expanded
## void setMinExpand ( int expand )

Sets a new minimum value, up to which the lower limit of the range of the slider values can be expanded. The lower limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Arguments

- *int* **expand** - The minimum value, up to which the lower limit of the slider value range can be expanded

## int getMinExpand () const

Returns the current minimum value, up to which the lower limit of the range of the slider values can be expanded. The lower limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Return value

Current minimum value, up to which the lower limit of the slider value range can be expanded
## void setMaxValue ( int value )

Sets a new maximum value of the slider.
### Arguments

- *int* **value** - The maximum value of the slider

## int getMaxValue () const

Returns the current maximum value of the slider.
### Return value

Current maximum value of the slider
## void setMinValue ( int value )

Sets a new minimum value of the slider.
### Arguments

- *int* **value** - The minimum value of the slider

## int getMinValue () const

Returns the current minimum value of the slider.
### Return value

Current minimum value of the slider
## void setButtonHeight ( int height )

Sets a new height of the slider handle, in pixels (for a vertical slider).
### Arguments

- *int* **height** - The height of the slider handle, in pixels

## int getButtonHeight () const

Returns the current height of the slider handle, in pixels (for a vertical slider).
### Return value

Current height of the slider handle, in pixels
## void setButtonWidth ( int width )

Sets a new width of the slider handle, in pixels (for a horizontal slider).
### Arguments

- *int* **width** - The width of the slider handle, in pixels

## int getButtonWidth () const

Returns the current width of the slider handle, in pixels (for a horizontal slider).
### Return value

Current width of the slider handle, in pixels
## void setOrientation ( int orientation )

Sets a new orientation of the slider: horizontal or vertical.
### Arguments

- *int* **orientation** - The orientation of the slider (horizontal or vertical)

## int getOrientation () const

Returns the current orientation of the slider: horizontal or vertical.
### Return value

Current orientation of the slider (horizontal or vertical)
## void setButtonColor ( vec4 color )

Sets a new color of the slider handle.
### Arguments

- *vec4* **color** - The color of the slider handle

## vec4 getButtonColor () const

Returns the current color of the slider handle.
### Return value

Current color of the slider handle
## void setBackgroundColor ( vec4 color )

Sets a new background color of the slider.
### Arguments

- *vec4* **color** - The background color of the slider

## vec4 getBackgroundColor () const

Returns the current background color of the slider.
### Return value

Current background color of the slider
---

## static WidgetSlider ( Gui gui , int min = 0 , int max = 100 , int value = 0 )

Constructor. Creates a slider with given properties (horizontal one by default) and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the slider will belong.
- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.

## static WidgetSlider ( int min = 0 , int max = 100 , int value = 0 )

Constructor. Creates a slider with given properties (horizontal one by default) and adds it to the Engine GUI.
### Arguments

- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
