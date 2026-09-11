# Unigine::WidgetMenuBar Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [horizontal menu bar](../../../code/gui/ui/ui_widgets.md#menubar).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/menubar.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetMenuBar Class

### Members

## int getNumItems () const

Returns the current number of items in the menu bar.
### Return value

Current number of items in the menu bar.
## int getSpaceY () const

Returns the current vertical space between menu items and menu borders.
### Return value

Current vertical space between menu items and menu borders, in pixels.
## int getSpaceX () const

Returns the current horizontal space between menu items and menu borders.
### Return value

Current horizontal space between menu items and menu borders, in pixels.
## void setSelectionColor ( vec4 color )

Sets a new color to be used to highlight the current selection for the widget.
### Arguments

- *vec4* **color** - The color in the RGBA format.

## vec4 getSelectionColor () const

Returns the current color to be used to highlight the current selection for the widget.
### Return value

Current color in the RGBA format.
---

## static WidgetMenuBar ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the menu bar will belong.
- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## static WidgetMenuBar ( int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the Engine GUI.
### Arguments

- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## void setItemData ( int item , string str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *string* **str** - Item text data to be set.

## string getItemData ( int item )

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data.
## void setItemEnabled ( int item , int enabled )

Sets an enabled flag for the item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **enabled** - **1** to enable the item; **0** - to disable it.

## int isItemEnabled ( int item )

Returns a value indicating if the given item is enabled.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

**1** if the item is enabled; otherwise - **0**.
## void setItemMenu ( int item , WidgetMenuBox menu )

Sets a menu for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_usc.md)* **menu** - Menu box.

## WidgetMenuBox getItemMenu ( int item )

Returns the menu of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Menu box.
## void setItemSpace ( int item , int space )

Sets a space between the given menu item and the next item located to the right.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *int* **space** - Space to set, in pixels.

## int getItemSpace ( int item )

Returns the space between the given menu item and the next item located to the right.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Space between items, in pixels.
## void setItemText ( int item , string str )

Sets a title for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *string* **str** - Menu title.

## string getItemText ( int item )

Returns the title of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Item title.
## void setSpace ( int x , int y )

Sets a space between menu items and between menu items and menu borders.
### Arguments

- *int* **x** - Horizontal space, in pixels. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space, in pixels. If a negative value is provided, 0 will be used instead.

## int addItem ( string str , WidgetMenuBox menu )

Adds the specified submenu (*MenuBox*) with a given title.
### Arguments

- *string* **str** - Menu title.
- *[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_usc.md)* **menu**

### Return value

Number of the added menu.
## void clear ( )

Removes all menus from the menu bar.
## void removeItem ( int item )

Removes a given item from the menu bar.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
