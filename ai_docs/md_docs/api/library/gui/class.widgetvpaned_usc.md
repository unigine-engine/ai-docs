# Unigine::WidgetVPaned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [horizontal movable bar](../../../code/gui/ui/ui_containers.md#vpaned) that divides the window into two resizable panes.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/vpaned.png)


This widget should contain exactly two children. If fewer children are provided, nothing will be drawn; if more children are provided, the application may crash.


## WidgetVPaned Class

### Members

---

## static WidgetVPaned ( Gui gui )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new container will belong.

## static WidgetVPaned ( )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the Engine GUI.
## void setFirstSize ( int size )

Sets the size of the first child.
### Arguments

- *int* **size** - Size of the first child in pixels.

## int getFirstSize ( )

Returns the size of the first child.
### Return value

Size of the first child in pixels.
## void setFixed ( int fixed )

Sets the number of the child with the fixed size. The default is 0.
### Arguments

- *int* **fixed** - Number of the child:

  - 0 - size of both children is not fixed.
  - 1 - size of the first child is fixed.
  - 2 - size of the second child is fixed.

## int getFixed ( )

Returns the number of the child with the fixed size.
### Return value

Number of the child. 0 means that the size of both children is not fixed.
## void setSecondSize ( int size )

Sets the size of the second child.
### Arguments

- *int* **size** - Size of the second child in pixels.

## int getSecondSize ( )

Returns the size of the second child.
### Return value

Size of the second child in pixels.
## void setValue ( int value )

Specifies how child widgets will be resized. The default is 0.
### Arguments

- *int* **value** - Value in range **[-32767; 32767]**. **-32767** means that during resize the upper child will remain fixed. **32767** means that during resize the lower child will remain fixed. **0** means that both children will be resized equally. Other values specify proportions, in which the children are resized.

## int getValue ( )

Returns a value specifying how child widgets will be resized.
### Return value

Value in range **[-32767; 32767]**. **-32767** means that during resize the upper child will remain fixed. **32767** means that during resize the lower child will remain fixed. **0** means that both children will be resized equally. Other values specify proportions, in which the children are resized.
