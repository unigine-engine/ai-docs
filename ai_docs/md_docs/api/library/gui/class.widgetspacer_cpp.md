# Unigine::WidgetSpacer Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [line spacer](../../../code/gui/ui/ui_widgets.md#hspacer): [horizontal](../../../code/gui/ui/ui_widgets.md#hspacer) or [vertical](../../../code/gui/ui/ui_widgets.md#vspacer) one.


The object of this class may look as follows:


![Horizontal spacer](../../../code/gui/ui/widgets/hspacer.png)

*Horizontal spacer*


![Vertical spacer](../../../code/gui/ui/widgets/vspacer.png)

*Vertical spacer*


## WidgetSpacer Class

### Members

## void setOrientation ( int orientation )

Sets a new orientation of the spacer: horizontal or vertical.
### Arguments

- *int* **orientation** - The orientation of the spacer (horizontal or vertical)

## int getOrientation () const

Returns the current orientation of the spacer: horizontal or vertical.
### Return value

Current orientation of the spacer (horizontal or vertical)
---

## static WidgetSpacerPtr create ( const Ptr < Gui > & gui )

Constructor. Creates a spacer and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the spacer will belong.

## static WidgetSpacerPtr create ( )

Constructor. Creates a spacer and adds it to the Engine GUI.
