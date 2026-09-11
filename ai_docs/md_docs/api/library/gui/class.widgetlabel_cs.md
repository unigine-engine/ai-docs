# Unigine::WidgetLabel Class (CS)

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

### Properties

## string Text

The text of the label.
## int TextAlign

The alignment of the label text. One of the following variables:
- [*GUI_ALIGN_LEFT*](../../../api/library/gui/class.gui_cs.md#ALIGN_LEFT)
- [*GUI_ALIGN_CENTER*](../../../api/library/gui/class.gui_cs.md#ALIGN_CENTER)
- [*GUI_ALIGN_RIGHT*](../../../api/library/gui/class.gui_cs.md#ALIGN_RIGHT)


### Members

---

## WidgetLabel ( Gui gui , string str = 0 )

Constructor. Creates a new text label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new label will belong.
- *string* **str** - Text of the label. This is an optional parameter.

## WidgetLabel ( string str = 0 )

Constructor. Creates a new text label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Text of the label. This is an optional parameter.
