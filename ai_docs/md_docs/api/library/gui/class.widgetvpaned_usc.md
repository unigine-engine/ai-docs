# Unigine::WidgetVPaned Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [horizontal movable bar](../../../code/gui/ui/ui_containers.md#vpaned) that divides the window into two resizable panes.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/vpaned.png)


This widget should contain exactly two children. If fewer children are provided, nothing will be drawn; if more children are provided, the application may crash.


## WidgetVPaned Class

### Members

## void setSecondSize ( int size )

Sets a new size of the second child.
### Arguments

- *int* **size** - The size of the second child

## int getSecondSize () const

Returns the current size of the second child.
### Return value

Current size of the second child
## void setFirstSize ( int size )

Sets a new size of the first child.
### Arguments

- *int* **size** - The size of the first child

## int getFirstSize () const

Returns the current size of the first child.
### Return value

Current size of the first child
## void setFixed ( int fixed )

Sets a new number of the child with the fixed size:
- 0 - size of both children is not fixed.
- 1 - size of the first child is fixed.
- 2 - size of the second child is fixed.


### Arguments

- *int* **fixed** - The number of the child with the fixed size

## int getFixed () const

Returns the current number of the child with the fixed size:
- 0 - size of both children is not fixed.
- 1 - size of the first child is fixed.
- 2 - size of the second child is fixed.


### Return value

Current number of the child with the fixed size
## void setValue ( int value )

Sets a new value specifying how the child widgets are resized, in range **[-32767; 32767]**. **-32767** means that during resize the upper child will remain fixed. **32767** means that during resize the lower child will remain fixed. **0** means that both children will be resized equally. Other values specify proportions, in which the children are resized.
### Arguments

- *int* **value** - The value specifying how the child widgets are resized

## int getValue () const

Returns the current value specifying how the child widgets are resized, in range **[-32767; 32767]**. **-32767** means that during resize the upper child will remain fixed. **32767** means that during resize the lower child will remain fixed. **0** means that both children will be resized equally. Other values specify proportions, in which the children are resized.
### Return value

Current value specifying how the child widgets are resized
---

## static WidgetVPaned ( Gui gui )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new container will belong.

## static WidgetVPaned ( )

Constructor. Creates a new vertical box with an ability to resize its children and adds it to the Engine GUI.
