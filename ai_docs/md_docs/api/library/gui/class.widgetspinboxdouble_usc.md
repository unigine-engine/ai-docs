# Unigine::WidgetSpinBoxDouble Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [spin box](../../../code/gui/ui/ui_widgets.md#spinbox) with double values.


### Usage Example


This example illustrates creation of a spinbox via code.


```cpp
// declaring editline and spinbox widgets
WidgetEditLine new_el;
WidgetSpinBoxDouble new_sb;

// callback to be fired on changing spinbox value
void sbChanged(WidgetSpinBoxDouble sb) {
	// printing the current spinbox value to the console
	log.message("Spinbox value changed: %d \n", sb.getValue());
	sb.setFocus();
}

int init() {
	// Write here code to be called on world initialization: initialize resources for your world scene during the world start.

	// ...

	// getting the GUI
	Gui gui = engine.getGui();

    // creating a new edit line and adding it to the GUI
	new_el = new WidgetEditLine(gui);
    gui.addChild(new_el, GUI_ALIGN_OVERLAP);

	// setting widget's position
    new_el.setPosition(100, 100);

    // creating a spinbox with the specified min and max values and adding it to the GUI
    new_sb = new WidgetSpinBoxDouble(gui, 0, 10, 5, 1);
    gui.addChild(new_sb, GUI_ALIGN_OVERLAP);

    // adding a callback to be fired on changing spinbox value
    new_sb.setCallback(GUI_CHANGED, functionid(sbChanged), new_sb);
    new_sb.setOrder(1);

    // attaching the spinbox to the edit line
    new_el.addAttach(new_sb);

    // setting initial spinbox value to 5
    new_sb.setValue(5);

	return 1;
}

// ...

```


## WidgetSpinBoxDouble Class

### Members

## void setValue ( double value )

Sets a new value of the spinbox.
### Arguments

- *double* **value** - The value of the spinbox

## double getValue () const

Returns the current value of the spinbox.
### Return value

Current value of the spinbox
## void setMaxExpand ( double expand )

Sets a new maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Arguments

- *double* **expand** - The maximum value, up to which the upper limit of the spinbox value range can be expanded

## double getMaxExpand () const

Returns the current maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Return value

Current maximum value, up to which the upper limit of the spinbox value range can be expanded
## void setMinExpand ( double expand )

Sets a new minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Arguments

- *double* **expand** - The minimum value, up to which the lower limit of the spinbox value range can be expanded

## double getMinExpand () const

Returns the current minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Return value

Current minimum value, up to which the lower limit of the spinbox value range can be expanded
## void setMaxValue ( double value )

Sets a new maximum value of the spinbox.
### Arguments

- *double* **value** - The maximum value of the spinbox

## double getMaxValue () const

Returns the current maximum value of the spinbox.
### Return value

Current maximum value of the spinbox
## void setMinValue ( double value )

Sets a new minimum value of the spinbox.
### Arguments

- *double* **value** - The minimum value of the spinbox

## double getMinValue () const

Returns the current minimum value of the spinbox.
### Return value

Current minimum value of the spinbox
## void setButtonColor ( vec4 color )

Sets a new color for the widget's button.
### Arguments

- *vec4* **color** - The color for the widget's button

## vec4 getButtonColor () const

Returns the current color for the widget's button.
### Return value

Current color for the widget's button
## void setStep ( double step )

Sets a new step of the spinbox.
### Arguments

- *double* **step** - The step of the spinbox

## double getStep () const

Returns the current step of the spinbox.
### Return value

Current step of the spinbox
---

## static WidgetSpinBoxDouble ( Gui gui , double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the spinbox will belong.
- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.

## static WidgetSpinBoxDouble ( double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the Engine GUI.
### Arguments

- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.
