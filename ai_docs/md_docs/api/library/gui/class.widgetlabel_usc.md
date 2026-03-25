# Unigine::WidgetLabel Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [text label](../../../code/gui/ui/ui_widgets.md#label).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/label.png)


#### See Also


- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
  -
  -
  -
  -


## WidgetLabel Class

### Members

---

## static WidgetLabel ( Gui gui , string str = 0 )

Constructor. Creates a new text label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new label will belong.
- *string* **str** - Text of the label. This is an optional parameter.

## static WidgetLabel ( string str = 0 )

Constructor. Creates a new text label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Text of the label. This is an optional parameter.

## void setText ( string text )

Sets a text for the label.
### Arguments

- *string* **text** - Label text.

## string getText ( )

Returns the text of the label.
### Return value

Label text.
## void setTextAlign ( int align )

Sets alignment of the label.
### Arguments

- *int* **align** - One of the following variables:

  - [*GUI_ALIGN_LEFT*](../../../api/library/gui/class.gui_usc.md#ALIGN_LEFT)
  - [*GUI_ALIGN_CENTER*](../../../api/library/gui/class.gui_usc.md#ALIGN_CENTER)
  - [*GUI_ALIGN_RIGHT*](../../../api/library/gui/class.gui_usc.md#ALIGN_RIGHT)

## int getTextAlign ( )

Returns alignment of the label.
### Return value

One of the following variables:
- [*GUI_ALIGN_LEFT*](../../../api/library/gui/class.gui_usc.md#ALIGN_LEFT)
- [*GUI_ALIGN_CENTER*](../../../api/library/gui/class.gui_usc.md#ALIGN_CENTER)
- [*GUI_ALIGN_RIGHT*](../../../api/library/gui/class.gui_usc.md#ALIGN_RIGHT)
