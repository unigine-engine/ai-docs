# Unigine::WidgetCheckBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates [checkboxes](../../../code/gui/ui/ui_widgets.md#checkbox). A set of checkboxes can be converted into a radio buttons group (that act as a single mutually exclusive control), if all the checkboxes are [attached](../../../api/library/gui/class.widget_usc.md#addAttach_Widget_cstr_int_int_void) to a certain one among them (for example, the first).


The object of this class may look as follows:


![Checkbox widget](../../../code/gui/ui/widgets/checkbox.png)


![Radio button widget](../../../code/gui/ui/widgets/radiobutton.png)


### See Also


- C++ sample
- C# Component sample


## WidgetCheckBox Class

### Members

## void setText ( string text )

Sets a new checkbox text label.
### Arguments

- *string* **text** - The checkbox text label

## const char * getText () const

Returns the current checkbox text label.
### Return value

Current checkbox text label
## void setChecked ( int checked )

Sets a new value indicating if the checkbox is selected.
### Arguments

- *int* **checked** - The true if the checkbox is selected, false otherwise

## int isChecked () const

Returns the current value indicating if the checkbox is selected.
### Return value

Current true if the checkbox is selected, false otherwise
## void setUncheckedColor ( vec4 color )

Sets a new color of the checkbox flag in the unchecked state.
### Arguments

- *vec4* **color** - The color of the checkbox flag in the unchecked state

## vec4 getUncheckedColor () const

Returns the current color of the checkbox flag in the unchecked state.
### Return value

Current color of the checkbox flag in the unchecked state
## void setCheckedColor ( vec4 color )

Sets a new color of the checkbox flag in the checked state.
### Arguments

- *vec4* **color** - The color of the checkbox flag in the checked state

## vec4 getCheckedColor () const

Returns the current color of the checkbox flag in the checked state.
### Return value

Current color of the checkbox flag in the checked state
---

## static WidgetCheckBox ( Gui gui , string str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new checkbox will belong.
- *string* **str** - Checkbox label. This is an optional parameter.

## static WidgetCheckBox ( string str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Checkbox label. This is an optional parameter.
