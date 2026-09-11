# Unigine::WidgetLabel Class (CPP)

**Header:** #include <UnigineWidgets.h>

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


### Example


The following code illustrates how to create a label widget and set its parameters.


```cpp
#include <UnigineWidgets.h>
using namespace Unigine;

/* .. */

// getting a pointer to the system GUI
GuiPtr gui = Gui::get();

// creating a label widget and setting up its caption
WidgetLabelPtr widget_label = WidgetLabel::create(gui, "Label text");

// setting a tooltip
widget_label->setToolTip("This is a label");

// rearranging label size
widget_label->arrange();

// setting label position
widget_label->setPosition(10, 10);

// adding created label widget to the system GUI
gui->addChild(widget_label, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

```


## WidgetLabel Class

### Members

## void setText ( const char * text )

Sets a new text of the label.
### Arguments

- *const char ** **text** - The text of the label

## const char * getText () const

Returns the current text of the label.
### Return value

Current text of the label
## void setTextAlign ( int align )

Sets a new alignment of the label text. One of the following variables:
- [*GUI_ALIGN_LEFT*](../../../api/library/gui/class.gui_cpp.md#ALIGN_LEFT)
- [*GUI_ALIGN_CENTER*](../../../api/library/gui/class.gui_cpp.md#ALIGN_CENTER)
- [*GUI_ALIGN_RIGHT*](../../../api/library/gui/class.gui_cpp.md#ALIGN_RIGHT)


### Arguments

- *int* **align** - The alignment of the label text

## int getTextAlign () const

Returns the current alignment of the label text. One of the following variables:
- [*GUI_ALIGN_LEFT*](../../../api/library/gui/class.gui_cpp.md#ALIGN_LEFT)
- [*GUI_ALIGN_CENTER*](../../../api/library/gui/class.gui_cpp.md#ALIGN_CENTER)
- [*GUI_ALIGN_RIGHT*](../../../api/library/gui/class.gui_cpp.md#ALIGN_RIGHT)


### Return value

Current alignment of the label text
---

## static WidgetLabelPtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a new text label and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new label will belong.
- *const char ** **str** - Text of the label. This is an optional parameter.

## static WidgetLabelPtr create ( const char * str = 0 )

Constructor. Creates a new text label and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Text of the label. This is an optional parameter.
