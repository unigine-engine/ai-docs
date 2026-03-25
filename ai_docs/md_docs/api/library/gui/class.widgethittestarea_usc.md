# Unigine::WidgetHitTestArea Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class is used to define the widget area in engine-style windows and borderless system windows intersected by a user-controlled cursor. If the hit test area type is "resize", the system automatically changes the cursor shape, if the hit test area is draggable, the window can be dragged by clicking and dragging this area.


In the following example, the system borders of the main window are disabled and 2 custom drag areas are added. The first area is located at the top of the window and the second area is in its center. For demonstration purposes, the background is enabled for both areas.


## WidgetHitTestArea Class

### Members

## int getHitTestResult () const

Returns the current hit test area type, one of the **[EngineWindow::ENGINE_WINDOW_HITTEST_*()](../../../api/library/gui/class.enginewindow_usc.md#HITTEST_INVALID)** values.
### Return value

Current hit test area type.
## void setBackgroundColor ( vec4 color )

Sets a new color for the background of the drag area to be used for debug purposes.
### Arguments

- *vec4* **color** - The background color.

## vec4 getBackgroundColor () const

Returns the current color for the background of the drag area to be used for debug purposes.
### Return value

Current background color.
## void setBackground ( int background )

Sets a new flag indicating if background rendering is enabled for the drag area for debug purposes.
### Arguments

- *int* **background** - The flag indicating background rendering status: 1 for enabled, 0 for disabled.

## int getBackground () const

Returns the current flag indicating if background rendering is enabled for the drag area for debug purposes.
### Return value

Current flag indicating background rendering status: 1 for enabled, 0 for disabled.
---

## WidgetHitTestArea ( Gui gui , int hit_test )

Constructor. Creates a hit test area widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the hit test area widget belongs.
- *int* **hit_test** - Hit test area type, one of the **[EngineWindow::ENGINE_WINDOW_HITTEST_*()](../../../api/library/gui/class.enginewindow_usc.md#HITTEST_INVALID)** values.

## WidgetHitTestArea ( int hit_test )

Constructor. Creates a hit test area widget of the specified type.
### Arguments

- *int* **hit_test** - Hit test area type, one of the **[EngineWindow::ENGINE_WINDOW_HITTEST_*()](../../../api/library/gui/class.enginewindow_usc.md#HITTEST_INVALID)** values.
