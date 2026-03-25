# Unigine::WidgetVPaned Class (CS)

**Inherits from:** Widget


This class creates a [horizontal movable bar](../../../code/gui/ui/ui_containers.md#vpaned) that divides the window into two resizable panes.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/vpaned.png)


This widget should contain exactly two children. If fewer children are provided, nothing will be drawn; if more children are provided, the application may crash.


## WidgetVPaned Class

### Properties

## int SecondSize

The size of the second child.
## int FirstSize

The size of the first child.
## int Fixed

The number of the child with the fixed size.
## int Value

The value specifying how child widgets will be resized.
### Members

---

## WidgetVPaned ( Gui gui )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new container will belong.

## WidgetVPaned ( )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the Engine GUI.
