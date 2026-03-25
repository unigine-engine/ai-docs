# Unigine::WidgetHPaned Class (CS)

**Inherits from:** WidgetVPaned


This class creates a [vertical movable bar](../../../code/gui/ui/ui_containers.md#hpaned) that divides the window into two resizable panes.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/hpaned.png)


This widget should contain exactly two children. If fewer children are provided, nothing will be drawn; if more children are provided, the application may crash.


## WidgetHPaned Class

### Members

---

## WidgetHPaned ( Gui gui )

Constructor. Creates a new horizontal box with an ability to resize its children and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new container will belong.

## WidgetHPaned ( )

Constructor. Creates a new horizontal box with an ability to resize its children and adds it to the Engine GUI.
