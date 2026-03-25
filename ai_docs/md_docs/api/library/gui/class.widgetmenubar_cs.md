# Unigine::WidgetMenuBar Class (CS)

**Inherits from:** Widget


This class creates a [horizontal menu bar](../../../code/gui/ui/ui_widgets.md#menubar).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/menubar.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetMenuBar Class

### Properties

## 🔒︎ int NumItems

The number of items in the menu bar.
## 🔒︎ int SpaceY

The vertical space between menu items and menu borders.
## 🔒︎ int SpaceX

The horizontal space between menu items and menu borders.
## vec4 SelectionColor

The color to be used to highlight the current selection for the widget.
### Members

---

## WidgetMenuBar ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the menu bar will belong.
- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## WidgetMenuBar ( int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the Engine GUI.
### Arguments

- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## void SetItemData ( int item , string str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *string* **str** - Item text data to be set.

## string GetItemData ( int item )

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data.
## void SetItemEnabled ( int item , bool enabled )

Sets an enabled flag for the item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *bool* **enabled** - true to enable the item; false - to disable it.

## bool IsItemEnabled ( int item )

Returns a value indicating if the given item is enabled.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

true if the item is enabled; otherwise - false.
## void SetItemMenu ( int item , WidgetMenuBox menu )

Sets a menu for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cs.md)* **menu** - Menu box.

## WidgetMenuBox GetItemMenu ( int item )

Returns the menu of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Menu box.
## void SetItemSpace ( int item , int space )

Sets a space between the given menu item and the next item located to the right.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *int* **space** - Space to set, in pixels.

## int GetItemSpace ( int item )

Returns the space between the given menu item and the next item located to the right.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Space between items, in pixels.
## void SetItemText ( int item , string str )

Sets a title for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *string* **str** - Menu title.

## string GetItemText ( int item )

Returns the title of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Item title.
## void SetSpace ( int x , int y )

Sets a space between menu items and between menu items and menu borders.
### Arguments

- *int* **x** - Horizontal space, in pixels. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space, in pixels. If a negative value is provided, 0 will be used instead.

## int AddItem ( string str )

Adds an empty menu with a given title.
### Arguments

- *string* **str** - Menu title.

### Return value

Number of the added menu.
## int AddItem ( string str , WidgetMenuBox menu )

Adds the specified submenu (*MenuBox*) with a given title.
### Arguments

- *string* **str** - Menu title.
- *[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cs.md)* **menu**

### Return value

Number of the added menu.
## void Clear ( )

Removes all menus from the menu bar.
## void RemoveItem ( int item )

Removes a given item from the menu bar.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
