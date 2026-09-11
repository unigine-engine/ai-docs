# Unigine::WidgetManipulatorScaler Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetManipulator


This class creates a scaling manipulator along three axes in form of a triangle.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cpp.md)
- C++ sample


## WidgetManipulatorScaler Class

---

## static WidgetManipulatorScalerPtr create ( const Ptr < Gui > & gui )

Constructor. Creates a scaling manipulator and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the scaler will belong.

## static WidgetManipulatorScalerPtr create ( )

Constructor. Creates a scaling manipulator and adds it to the Engine GUI.
