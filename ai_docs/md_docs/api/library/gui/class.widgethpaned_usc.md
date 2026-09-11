# Unigine::WidgetHPaned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetVPaned


This class creates a [vertical movable bar](../../../code/gui/ui/ui_containers.md#hpaned) that divides the window into two resizable panes.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/hpaned.png)


This widget should contain exactly two children. If fewer children are provided, nothing will be drawn; if more children are provided, the application may crash.


## WidgetHPaned Class

---

## static WidgetHPaned ( Gui gui )

Constructor. Creates a new horizontal box with an ability to resize its children and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new container will belong.

## static WidgetHPaned ( )

Constructor. Creates a new horizontal box with an ability to resize its children and adds it to the Engine GUI.
