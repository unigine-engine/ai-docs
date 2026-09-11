# Unigine::WidgetMenuBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [menu box](../../../code/gui/ui/ui_widgets.md#menubox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/menubox.png)


A menu box can be either stand-alone or attached to a [menu bar](../../../api/library/gui/class.widgetmenubar_cpp.md). In the first case, it needs to be handled manually. By using this widget, you can do the following:


- Create hierarchical menus.
- Use the other widgets as menu items (See the [example](../../../code/gui/ui/ui_widgets.md#menubox_widget)).


### See Also


- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
- The [Widgets](../../../code/gui/ui/ui_widgets.md#menubox) article providing details on menubox features


## WidgetMenuBox Class

### Members

## const char * getCurrentItemData () const

Returns the current text data of the selected item (the last clicked item). The data can be used as a text identifier of the item (instead of using the number of the item).
### Return value

Current text data of the selected item, or nullptr in case no item is selected.
## const char * getCurrentItemText () const

Returns the current text of the selected item (the last clicked item).
### Return value

Current text of the selected item, or nullptr in case no item is selected.
## void setCurrentItem ( int item )

Sets a new item selection (the last clicked item number). When nothing is selected the value is -1 (setting the selection to a non-existent item number will also reset the value to -1).
### Arguments

- *int* **item** - The selected item number.

## int getCurrentItem () const

Returns the current item selection (the last clicked item number). When nothing is selected the value is -1 (setting the selection to a non-existent item number will also reset the value to -1).
### Return value

Current selected item number.
## int getNumItems () const

Returns the current total number of items in the menu.
### Return value

Current total number of items in the menu.
## void setTexture ( const char * texture )

Sets a new path to the texture file with mini icons to be used with the list items. The texture is a vertical strip of square icons.
### Arguments

- *const char ** **texture** - The path to the texture file to be used.

## const char * getTexture () const

Returns the current path to the texture file with mini icons to be used with the list items. The texture is a vertical strip of square icons.
### Return value

Current path to the texture file to be used.
## int getSpaceY () const

Returns the current vertical space between menu items, and between items and the menu borders.
### Return value

Current vertical space between menu items and menu borders, in pixels.
## int getSpaceX () const

Returns the current horizontal space between menu items, and between items and the menu borders.
### Return value

Current horizontal space between menu items and menu borders, in pixels.
## void setBorderColor ( const Math:: vec4 & color )

Sets a new border color of the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color in the RGBA format.

## Math:: vec4 getBorderColor () const

Returns the current border color of the widget.
### Return value

Current color in the RGBA format.
## void setSelectionColor ( const Math:: vec4 & color )

Sets a new color to be used to highlight the current selection.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color in the RGBA format.

## Math:: vec4 getSelectionColor () const

Returns the current color to be used to highlight the current selection.
### Return value

Current color in the RGBA format.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color to be used.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color in the RGBA format.

## Math:: vec4 getBackgroundColor () const

Returns the current background color to be used.
### Return value

Current color in the RGBA format.
## void setCurrentItemHighlight ( bool highlight )

Sets a new highlight flag of the item that is clicked last.
### Arguments

- *bool* **highlight** - Set **true** to enable highlight flag; **false** - to disable it.

## bool isCurrentItemHighlight () const

Returns the current highlight flag of the item that is clicked last.
### Return value

**true** if highlight flag is enabled ; otherwise **false**.
## void setCurrentItemColor ( const Math:: vec4 & color )

Sets a new color of the highlight for item that is clicked last. The **[highlight state](#setCurrentItemHighlight_int_void)** should be enabled.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color in the RGBA format.

## Math:: vec4 getCurrentItemColor () const

Returns the current color of the highlight for item that is clicked last. The **[highlight state](#setCurrentItemHighlight_int_void)** should be enabled.
### Return value

Current color in the RGBA format.
---

## static WidgetMenuBoxPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates an empty menu box with specified spacing between menu items as well as items and menu borders and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the menu will belong.
- *int* **x** - Horizontal space.
- *int* **y** - Vertical space.

## static WidgetMenuBoxPtr create ( int x = 0 , int y = 0 )

Constructor. Creates an empty menu box with specified spacing between menu items as well as items and menu borders and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space.
- *int* **y** - Vertical space.

## void setImage ( const Ptr < Image > & image )

Sets an image with mini icons to be used with items. The image is a vertical strip of square icons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Gets the image with mini icons that are used with menu items.
### Return value

Image with mini icons (the vertical strip of square icons).
## void setItemData ( int item , const char * str )

Sets the text data for a given item. The data can be used as a text identifier of the item (instead of using the number of the item).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Item text data to set.

## const char * getItemData ( int item ) const

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data.
## void setItemEnabled ( int item , bool enabled )

Sets a value indicating if a given item is enabled (i.e. can be clicked).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *bool* **enabled** - true to enable the item, false to disable it.

## int isItemEnabled ( int item ) const

Returns a value indicating if a given item is enabled (i.e. can be clicked).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Positive number if the item is enabled; otherwise, 0.
## void setItemSelectable ( int item , int selectable )

Sets a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selectable** - 1 to set the item as selectable; otherwise, 0.

## int isItemSelectable ( int item ) const

Returns a value indicating if the given item can be selected. By default, the item is selectable.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

1 if the item is selectable; otherwise, 0.
## void setItemSeparator ( int item , int separator )

Adds or removes a separator after a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **separator** - Positive number to add a separator, 0 to remove it.

## int isItemSeparator ( int item ) const

Checks whether a separator is placed after the given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Positive number if separator is placed; otherwise, 0.
## void setItemSpace ( int item , int space )

Sets a space between the given menu item and the next item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu bar items.
- *int* **space** - Item space to set.

## int getItemSpace ( int item ) const

Returns the space between the given menu item and the next item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Space between items, in pixels.
## void setItemText ( int item , const char * str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Item text.

## const char * getItemText ( int item ) const

Returns the text of a given item in range from 0 to the total number of items.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text.
## void setItemTexture ( int item , int texture )

Sets an icon for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

## int getItemTexture ( int item ) const

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Zero-based ID of the icon (i.e. number of the icon in the icon texture).
## void setItemToolTip ( int item , const char * str )

Sets a new tooltip for the given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Text of a tooltip to set.

## const char * getItemToolTip ( int item ) const

Returns the tooltip of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Text of the item tooltip.
## void setItemWidget ( int item , const Ptr < Widget > & w )

Sets a widget for the given item of the menu.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of menu items.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - A widget to be used as a menu item.

## Ptr < Widget > getItemWidget ( int item ) const

Returns a widget [set](#setItemWidget_int_Widget_void) for the given item of the menu.
### Arguments

- *int* **item** - Item number on range from 0 to the total number of menu items.

### Return value

A widget used as an item.
## void setSpace ( int x , int y )

Sets a space between menu items and between them and menu borders.
### Arguments

- *int* **x** - Horizontal space. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is provided, 0 will be used instead.

## int addItem ( const char * str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *const char ** **str** - Item text.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture). -1 means that an item has no icon.

### Return value

Number of the added item.
## void clear ( )

Removes all items from the menu.
## void removeItem ( int item )

Removes a given item from the menu.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

## void resetCurrentItem ( )

Resets the current item selection (the last clicked item).
