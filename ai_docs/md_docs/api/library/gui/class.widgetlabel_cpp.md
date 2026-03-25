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

## void setText ( const char * text )

Sets a text for the label.
### Arguments

- *const char ** **text** - Label text.

## const char * getText ( ) const

Returns the text of the label.
### Return value

Label text.
## void setTextAlign ( int align )

Sets alignment of the label.
### Arguments

- *int* **align** - One of the Gui:: Enumeration with ALIGN_* prefixes.

## int getTextAlign ( ) const

Returns alignment of the label.
### Return value

Alignment of the label: one of the Gui:: Enumeration with ALIGN_* prefixes.
