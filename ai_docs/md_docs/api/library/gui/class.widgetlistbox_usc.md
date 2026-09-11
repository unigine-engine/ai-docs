# Unigine::WidgetListBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

Returns the current
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

- *bool* **enabled** - Set **true** to enable ; **false** - to disable it.

## bool isIconsEnabled () const

Returns the current value indicating if the icons display is enabled.
### Return value

**true** if is enabled ; otherwise **false**.
## void setSelectionColor ( )

Sets a new color used to highlight the current selection for the widget.
### Arguments

- **color** - The four-component vector specifying the color in the RGBA format.

## getSelectionColor () const

Returns the current color used to highlight the current selection for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setTexture ( )

Sets a new path to the texture with mini-icons, which are used with the list items.
### Arguments

- **texture** - The path to the texture file.

## const char * getTexture () const

Returns the current path to the texture with mini-icons, which are used with the list items.
### Return value

Current path to the texture file.
## void setMultiSelection ( bool selection )

Sets a new
### Arguments

- *bool* **selection** - Set **true** to enable ; **false** - to disable it.

## bool isMultiSelection () const

Returns the current
### Return value

**true** if is enabled ; otherwise **false**.
---

## static WidgetListBox ( Gui gui )

Constructor. Creates an empty list box and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new list box will belong.

## static WidgetListBox ( )

Constructor. Creates an empty list box and adds it to the Engine GUI.
## string getCurrentItemData ( )

Returns the [text data](#setItemData_int_cstr_void) of item, which is currently in focus. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## string getCurrentItemText ( )

Returns the text of item, which is currently in focus.
### Return value

Item text.
## void setImage ( Image image )

Sets an image with mini-icons to be used with list items. The image is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getImage ( )

Returns the image with mini-icons, which are used with the list items.
### Return value

Image with mini-icons (the vertical strip of square icons).
## void setItemColor ( int item , vec4 color )

Sets a custom color for a given item.
### Arguments

- *int* **item** - Item number.
- *vec4* **color** - Color to set.

## vec4 getItemColor ( int item )

Returns a color set to a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Color.
## void setItemData ( int item , string str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *string* **str** - Item text data to be set.

## string getItemData ( int item )

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

## int isItemSelectable ( int item )

Returns a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number.

### Return value

**1** if the item is selectable; otherwise, **0**.
## void setItemSelected ( int item , int selected )

Selects or deselects a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selected** - 1 to select the item, 0 to deselect it.

## int isItemSelected ( int item )

Returns a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

**1** if the item is selected; otherwise, **0**.
## void setItemText ( int item , string str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item number.
- *string* **str** - Item text.

## string getItemText ( int item )

Returns the text of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Item text.
## void setItemTexture ( int item , int texture )

Sets an icon for a given item.
### Arguments

- *int* **item** - Item number.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

## int getItemTexture ( int item )

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Zero-based ID of the icon (i.e. number of the icon in the icon texture).
## int getSelectedItem ( int num )

Returns ID of a selected item (multi-selection mode).
### Arguments

- *int* **num** - Number in the list of the selected items in range from 0 to the total number of the selected items.

### Return value

ID of a selected item.
## int addItem ( string str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *string* **str** - Item text.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

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

- *int* **item** - Item number.

## void setItemIcon ( int item , Texture texture )

Sets the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Icon to be set.

## Texture getItemIcon ( int item )

Returns the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Icon of the item.
