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

## void setButtonHeight ( int height )

Sets the height of the slider handle in pixels (for a vertical slider).
### Arguments

- *int* **height** - Height of the handle in pixels.

## int getButtonHeight ( )

Returns the height of the slider handle in pixels (for a vertical slider).
### Return value

Height of the handle in pixels.
## void setButtonWidth ( int width )

Sets width of the slider handle in pixels (for a horizontal slider).
### Arguments

- *int* **width** - Width of the handle in pixels.

## int getButtonWidth ( )

Returns the width of the slider handle in pixels (for a horizontal slider).
### Return value

Width of the handle in pixels.
## void setMaxExpand ( int expand )

Sets the maximum value, up to which the upper limit of the range of the slider values can be expanded.
### Arguments

- *int* **expand** - Maximum value, up to which the slider's upper limit can be raised.

## int getMaxExpand ( )

Returns the current maximum value, up to which the upper limit of the range of the slider values can be expanded.
> **Notice:** The upper limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void)  to an editline with the [*GUI_ATTACH_MAX_EXPAND*](../../../api/library/gui/class.gui_usc.md#ATTACH_MAX_EXPAND) flag.

See also the [*setMaxExpand()*](#setMaxExpand_int_void) function.
### Return value

Maximum value, up to which the slider's upper limit can be raised.
## void setMaxValue ( int value )

Sets the maximum value for the slider.
### Arguments

- *int* **value** - Maximum value.

## int getMaxValue ( )

Returns the current maximum value of the slider.
> **Notice:** The value returned by this function may differ from the value set via [*setMaxValue()*](#setMaxValue_int_void). See The [*setMaxExpand()*](#setMaxExpand_int_void) function for more details.


### Return value

Maximum value.
## void setMinExpand ( int expand )

Sets the minimum value, up to which the lower limit of the range of the slider values can be expanded.
### Arguments

- *int* **expand** - Minimum value, up to which the slider's lower limit can be dropped.

## int getMinExpand ( )

Returns the minimum value, up to which the lower limit of the range of the slider values can be expanded.
> **Notice:** The lower limit of the slider can be expanded only if the slider is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void)  to an editline with the [*GUI_ATTACH_MIN_EXPAND*](../../../api/library/gui/class.gui_usc.md#ATTACH_MIN_EXPAND) flag.

See also the [*setMinExpand()*](#setMinExpand_int_void) function.
### Return value

Minimum value, up to which the slider's lower limit can be dropped.
## void setMinValue ( int value )

Sets the minimum value for the slider.
### Arguments

- *int* **value** - Minimum value.

## int getMinValue ( )

Returns the minimum value of the slider.
> **Notice:** The value returned by this function may differ from the value set via [*setMinValue()*](#setMinValue_int_void). See The [*setMinExpand()*](#setMinExpand_int_void) function for more details.


### Return value

Minimum value.
## void setOrientation ( int orientation )

Sets orientation of the slider: horizontal (by default) or vertical one.
### Arguments

- *int* **orientation** - 1 to set horizontal orientation; 0 to set vertical one.

## int getOrientation ( )

Returns the current orientation of the slider: horizontal or vertical one.
### Return value

1 if the orientation is vertical; 0 if it is horizontal.
## void setValue ( int value )

Sets a new current value for the slider, i.e. its position.
### Arguments

- *int* **value** - Slider value.

## int getValue ( )

Returns the current value of the slider, i.e. its position.
### Return value

Current slider value.
## void setBackgroundColor ( vec4 color )

Sets the background color to be used for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBackgroundColor ( )

Returns the current background color used for the widget.
### Return value

The four-component vector specifying the color in the RGBA format.
## void setButtonColor ( vec4 color )

Sets the color for the widget's button.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getButtonColor ( )

Returns the current color for the widget's button.
### Return value

The four-component vector specifying the color in the RGBA format.
