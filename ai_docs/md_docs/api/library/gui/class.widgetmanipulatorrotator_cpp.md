# Unigine::WidgetManipulatorRotator Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetManipulator


This class creates a rotation manipulator around three axes in form of a sphere.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cpp.md)
- C++ sample


## WidgetManipulatorRotator Class

---

## static WidgetManipulatorRotatorPtr create ( const Ptr < Gui > & gui )

Constructor. Creates a rotating manipulator and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the rotator will belong.

## static WidgetManipulatorRotatorPtr create ( )

Constructor. Creates a rotating manipulator and adds it to the Engine GUI.
