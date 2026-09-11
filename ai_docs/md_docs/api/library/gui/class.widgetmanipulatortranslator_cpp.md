# Unigine::WidgetManipulatorTranslator Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetManipulator


This class creates a mover manipulator along three axes with arrows at the end.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cpp.md)
- C++ sample


## WidgetManipulatorTranslator Class

---

## static WidgetManipulatorTranslatorPtr create ( const Ptr < Gui > & gui )

Constructor. Creates a moving manipulator and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the translator will belong.

## static WidgetManipulatorTranslatorPtr create ( )

Constructor. Creates a moving manipulator and adds it to the Engine GUI.
