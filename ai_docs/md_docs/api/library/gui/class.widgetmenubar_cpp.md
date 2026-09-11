# Unigine::WidgetMenuBar Class (CPP)

**Header:** #include <UnigineWidgets.h>

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
## void setSelectionColor ( const Math:: vec4 & color )

Sets a new color to be used to highlight the current selection for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color in the RGBA format.

## Math:: vec4 getSelectionColor () const

Returns the current color to be used to highlight the current selection for the widget.
### Return value

Current color in the RGBA format.
---

## static WidgetMenuBarPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the menu bar will belong.
- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## static WidgetMenuBarPtr create ( int x = 0 , int y = 0 )

Constructor. Creates an empty menu bar and adds it to the Engine GUI.
### Arguments

- *int* **x** - Offset along the X axis.
- *int* **y** - Offset along the Y axis.

## void setItemData ( int item , const char * str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *const char ** **str** - Item text data to be set.

## const char * getItemData ( int item ) const

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data.
## void setItemEnabled ( int item , bool enabled )

Sets an enabled flag for the item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *bool* **enabled** - true to enable the item; false - to disable it.

## bool isItemEnabled ( int item ) const

Returns a value indicating if the given item is enabled.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

true if the item is enabled; otherwise - false.
## void setItemMenu ( int item , const Ptr < WidgetMenuBox > & menu )

Sets a menu for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cpp.md)> &* **menu** - Menu box.

## Ptr < WidgetMenuBox > getItemMenu ( int item ) const

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

## int getItemSpace ( int item ) const

Returns the space between the given menu item and the next item located to the right.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.

### Return value

Space between items, in pixels.
## void setItemText ( int item , const char * str )

Sets a title for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *const char ** **str** - Menu title.

## const char * getItemText ( int item ) const

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

## int addItem ( const char * str )

Adds an empty menu with a given title.
### Arguments

- *const char ** **str** - Menu title.

### Return value

Number of the added menu.
## int addItem ( const char * str , const Ptr < WidgetMenuBox > & menu )

Adds the specified submenu (*MenuBox*) with a given title.
### Arguments

- *const char ** **str** - Menu title.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cpp.md)> &* **menu** - Submenu (*MenuBox*).

### Return value

Number of the added menu.
## void clear ( )

Removes all menus from the menu bar.
## void removeItem ( int item )

Removes a given item from the menu bar.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
