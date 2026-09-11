# Unigine::WidgetGridBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetVBox


This class creates a [grid box](../../../code/gui/ui/ui_containers.md#gridbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/gridbox.png)


## WidgetGridBox Class

### Members

## void setNumColumns ( int columns )

Sets a new number of columns in the grid.
### Arguments

- *int* **columns** - The number of columns.

## int getNumColumns () const

Returns the current number of columns in the grid.
### Return value

Current number of columns.
---

## static WidgetGridBox ( Gui gui , int num = 2 , int x = 0 , int y = 0 )

Constructor. Creates a grid box with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new box will belong.
- *int* **num** - Number of columns in the grid. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetGridBox ( int num = 2 , int x = 0 , int y = 0 )

Constructor. Creates a grid box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **num** - Number of columns in the grid. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void setColumnRatio ( int num , int ratio )

Sets the width-to-height ratio of the specified column.
### Arguments

- *int* **num** - Column number in range from 0 to the total number of columns.
- *int* **ratio** - Width-to-height ratio.

## int getColumnRatio ( int num )

Returns the current width-to-height ratio of the specified column.
### Arguments

- *int* **num** - Column number in range from 0 to the total number of columns.

### Return value

Width-to-height ratio.
