# Unigine::WidgetCheckBox Class (CS)

**Inherits from:** Widget


This class creates [checkboxes](../../../code/gui/ui/ui_widgets.md#checkbox). A set of checkboxes can be converted into a radio buttons group (that act as a single mutually exclusive control), if all the checkboxes are [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to a certain one among them (for example, the first).


The object of this class may look as follows:


![Checkbox widget](../../../code/gui/ui/widgets/checkbox.png)


![Radio button widget](../../../code/gui/ui/widgets/radiobutton.png)


### See Also


- C++ sample
- C# Component sample


## WidgetCheckBox Class

### Properties

## string Text

The checkbox text label.
## bool Checked

The value indicating if the checkbox is selected.
## vec4 UncheckedColor

The color of the checkbox flag in the unchecked state.
## vec4 CheckedColor

The color of the checkbox flag in the checked state.
### Members

---

## WidgetCheckBox ( Gui gui , string str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new checkbox will belong.
- *string* **str** - Checkbox label. This is an optional parameter.

## WidgetCheckBox ( string str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Checkbox label. This is an optional parameter.
