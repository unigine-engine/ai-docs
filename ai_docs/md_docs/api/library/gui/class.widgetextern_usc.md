# Unigine::WidgetExtern Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


Interface for widget extern handling. It serves to create external user widgets of integrate GUI systems inside the engine via the Plugin interface.


#### See Also


- C++ sample


## WidgetExtern Class

---

## static WidgetExtern ( Gui gui , int class_id )

Constructor. Creates a custom user-defined widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - Gui instance, to which the widget belongs.
- *int* **class_id** - Unique class ID.

## static WidgetExtern ( int class_id )

Constructor. Creates a custom user-defined widget and adds it to the Engine GUI.
### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( )

Returns a unique class ID.
### Return value

Unique class ID if the widget exists; otherwise, 0.
