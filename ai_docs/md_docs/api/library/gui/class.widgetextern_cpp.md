# Unigine::WidgetExtern Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


Interface for widget extern handling. It serves to create external user widgets of integrate GUI systems inside the engine via the Plugin interface.


#### See Also


- C++ sample


## WidgetExtern Class

---

## static WidgetExternPtr create ( const Ptr < Gui > & gui , int class_id )

Constructor. Creates a custom user-defined widget and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - Gui instance, to which the widget belongs.
- *int* **class_id** - Unique class ID.

## static WidgetExternPtr create ( int class_id )

Constructor. Creates a custom user-defined widget and adds it to the Engine GUI.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( ) const

Returns a unique class ID.
### Return value

Unique class ID if the widget exists; otherwise, 0.
