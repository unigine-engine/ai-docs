# Unigine::WidgetHBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetVBox


This class creates a [single horizontal row](../../../code/gui/ui/ui_containers.md#hbox) container.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/hbox.png)


## WidgetHBox Class

---

## static WidgetHBoxPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates a horizontal box with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetHBoxPtr create ( int x = 0 , int y = 0 )

Constructor. Creates a horizontal box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.
