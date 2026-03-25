# Unigine::WidgetListBox Class (CS)

**Inherits from:** Widget


This class creates a [list box](../../../code/gui/ui/ui_widgets.md#listbox), which is multiple line text box where [more than one](#setMultiSelection_int_void) item can be picked.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/listbox.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetListBox Class

### Properties

## 🔒︎ int NumSelectedItems

The number of selected items in the box.
## int CurrentItem

The number of the item, which is currently in focus.
## 🔒︎ int NumItems

The total number of items in the list box.
## int IconsResolution

The resolution of the icons.
## bool IconsAlphaEnabled

The value indicating if the alpha channel of the icons is enabled.
## bool IconsEnabled

The value indicating if the icons display is enabled.
## vec4 SelectionColor

The color used to highlight the current selection for the widget.
## string Texture

The path to the texture with mini-icons, which are used with the list items.
## bool MultiSelection

The value indicating if multiple selection of items is enabled. The default is 0.
### Members

---

## WidgetListBox ( Gui gui )

Constructor. Creates an empty list box and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new list box will belong.

## WidgetListBox ( )

Constructor. Creates an empty list box and adds it to the Engine GUI.
## string GetCurrentItemData ( )

Returns the [text data](#setItemData_int_cstr_void) of item, which is currently in focus. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## string GetCurrentItemText ( )

Returns the text of item, which is currently in focus.
### Return value

Item text.
## void SetImage ( Image image )

Sets an image with mini-icons to be used with list items. The image is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetImage ( )

Returns the image with mini-icons, which are used with the list items.
### Return value

Image with mini-icons (the vertical strip of square icons).
## void SetItemColor ( int item , vec4 color )

Sets a custom color for a given item.
### Arguments

- *int* **item** - Item number.
- *vec4* **color** - Color to set.

## vec4 GetItemColor ( int item )

Returns a color set to a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Item color.
## void SetItemData ( int item , string str )

Sets the text data for the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *string* **str** - Item text data to be set.

## string GetItemData ( int item )

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified number. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Item text data if the item is in range from 0 to the total number of items; otherwise, NULL.
## void SetItemSelectable ( int item , int selectable )

Sets a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selectable** - 1 to set the item as selectable; otherwise, 0.

## int IsItemSelectable ( int item )

Returns a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item number.

### Return value

1 if the item is selectable; otherwise, 0.
## void SetItemSelected ( int item , int selected )

Sets a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *int* **selected** - 1 to select the item, 0 to deselect it.

## int IsItemSelected ( int item )

Returns a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

1 if the item is selected; otherwise, 0.
## void SetItemText ( int item , string str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item number.
- *string* **str** - Item text.

## string GetItemText ( int item )

Returns the text of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Item text.
## void SetItemTexture ( int item , int texture )

Sets an icon for a given item.
### Arguments

- *int* **item** - Item number.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

## int GetItemTexture ( int item )

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Zero-based ID of the icon (i.e. number of the icon in the icon texture).
## int GetSelectedItem ( int num )

Returns ID of the selected item (multi-selection mode).
### Arguments

- *int* **num** - Number in the list of the selected items in range from 0 to the total number of the selected items.

### Return value

ID of a selected item.
## int AddItem ( string str , int texture = -1 )

Adds a new item with a given text and an icon. By default, a new item is not selected.
### Arguments

- *string* **str** - Item text.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

### Return value

Number of the added item.
## void Clear ( )

Removes all items from the list box.
## void ClearSelection ( )

Clears list of selected items.
## void RemoveItem ( int item )

Removes a given item from the list box.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

## void ShowItem ( int item )

Scrolls a list box so that a given item is visible.
### Arguments

- *int* **item** - Item number.

## void SetItemIcon ( int item , Texture texture )

Sets the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Icon to be set.

## Texture GetItemIcon ( int item )

Returns the icon for a given list item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Icon of the item.
