# Unigine::WidgetListBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [list box](../../../code/gui/ui/ui_widgets.md#listbox), which is multiple line text box where [more than one](#setMultiSelection_int_void) item can be picked.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/listbox.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetListBox Class

### Members

## int getNumSelectedItems () const

Returns the current number of selected items in the box.
### Return value

Current number of selected items.
## void setCurrentItem ( int item )

Sets a new number of the item, which is currently in focus.
### Arguments

- *int* **item** - The item number.

## int getCurrentItem () const

Returns the current number of the item, which is currently in focus.
### Return value

Current item number.
## int getNumItems () const

Returns the current total number of items in the list box.
### Return value

Current number of items.
## void setIconsResolution ( int resolution )

Sets a new resolution of the icons.
### Arguments

- *int* **resolution** - The icon resolution.

## int getIconsResolution () const

Returns the current resolution of the icons.
### Return value

Current icon resolution.
## void setIconsAlphaEnabled ( bool enabled )

Sets a new value indicating if the alpha channel of the icons is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable use of the alpha channel of the icons; **false** - to disable it.

## bool isIconsAlphaEnabled () const

Returns the current value indicating if the alpha channel of the icons is enabled.
### Return value

**true** if use of the alpha channel of the icons is enabled ; otherwise **false**.
## void setIconsEnabled ( bool enabled )

Sets a new value indicating if the icons display is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable icons displaying; **false** - to disable it.

## bool isIconsEnabled () const

Returns the current value indicating if the icons display is enabled.
### Return value

**true** if icons displaying is enabled ; otherwise **false**.
## void setSelectionColor ( const Math:: vec4 & color )

Sets a new color used to highlight the current selection for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getSelectionColor () const

Returns the current color used to highlight the current selection for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setTexture ( const char * texture )

Sets a new path to the texture with mini-icons, which are used with the list items.
### Arguments

- *const char ** **texture** - The path to the texture file.

## const char * getTexture () const

Returns the current path to the texture with mini-icons, which are used with the list items.
### Return value

Current path to the texture file.
## void setMultiSelection ( bool selection )

Sets a new value indicating if multiple selection of items is enabled. The default is 0.
### Arguments

- *bool* **selection** - Set **true** to enable selection of several items at once; **false** - to disable it.

## bool isMultiSelection () const

Returns the current value indicating if multiple selection of items is enabled. The default is 0.
### Return value

**true** if selection of several items at once is enabled ; otherwise **false**.
---

## static WidgetListBoxPtr create ( const Ptr < Gui > & gui )

Constructor. Creates an empty list box and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new list box will belong.

## static WidgetListBoxPtr create ( )

Constructor. Creates an empty list box and adds it to the Engine GUI.
## const char * getCurrentItemData ( ) const

Returns the [text data](#setItemData_int_cstr_void) of item, which is currently in focus. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## const char * getCurrentItemText ( ) const

Returns the text of item, which is currently in focus.
### Return value

Item text.
## void setImage ( const Ptr < Image > & image )

Sets an image with mini-icons to be used with list items. The image is a vertical strip of square icons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Returns the image with mini-icons, which are used with the list items.
### Return value

Image with mini-icons (the vertical strip of square icons).
## void setItemColor ( int item , const Math:: vec4 & color )

Sets a custom color for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to set.

## Math:: vec4 getItemColor ( int item ) const

Returns a color set to a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item color.
## void setItemData ( int item , const char * str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Item text data to be set.

## const char * getItemData ( int item ) const

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data if the item is in range from 0 to the total number of items; otherwise, NULL.
## void setItemSelectable ( int item , int selectable )

Sets a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selectable** - 1 to set the item as selectable; otherwise, 0.

## int isItemSelectable ( int item ) const

Returns a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

1 if the item is selectable; otherwise, 0.
## void setItemSelected ( int item , int selected )

Sets a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selected** - 1 to select the item, 0 to deselect it.

## int isItemSelected ( int item ) const

Returns a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

1 if the item is selected; otherwise, 0.
## void setItemText ( int item , const char * str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Item text to be set.

## const char * getItemText ( int item ) const

Returns the text of a given item.
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
## int getSelectedItem ( int num ) const

Returns ID of the selected item (multi-selection mode).
### Arguments

- *int* **num** - Number in the list of the selected items in range from 0 to the total number of the selected items.

### Return value

ID of a selected item.
## int addItem ( const char * str , int texture = -1 )

Adds a new item with a given text and an icon. By default, a new item is not selected.
### Arguments

- *const char ** **str** - Item text.
- *int* **texture** - Zero-based ID of the icon. -1 means that an item has no icon.

### Return value

Number of the added item.
## void clear ( )

Removes all items from the list box.
## void clearSelection ( )

Clears list of selected items.
## void removeItem ( int item )

Removes a given item from the list box.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

## void showItem ( int item )

Scrolls a list box so that a given item is visible.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

## void setItemIcon ( int item , const Ptr < Texture > & texture )

Sets the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Icon to be set.

## Ptr < Texture > getItemIcon ( int item ) const

Returns the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Icon of the item.
