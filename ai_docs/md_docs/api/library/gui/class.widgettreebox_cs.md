# Unigine::WidgetTreeBox Class (CS)

**Inherits from:** Widget


This class creates a [box with a tree-like hierarchy](../../../code/gui/ui/ui_widgets.md#treebox). For example:

```cpp
int init() {

Gui gui = engine.getGui();

WidgetTreeBox tree = new WidgetTreeBox(gui);

tree.addItem("1st item");  // Add items into the tree.
tree.addItem("2nd item");
tree.addItem("3rd item");
tree.addItem("4th item");

tree.addItemChild(0,1);   // Make a 2nd item a child of the 1st one.
tree.setItemFolded(0,1);  // Collapse children of the 1st child.

WidgetWindow window = new WidgetWindow(gui);  // Create a window.
gui.addChild(window,GUI_ALIGN_CENTER);

window.addChild(tree,GUI_ALIGN_CENTER); // Render a tree in the window.

return 1;
}

```


As a result, you will get:


![](widgettreebox.png)

*WidgetTreeBox in a window*


### See Also


- C++ sample
- C# Component sample


## WidgetTreeBox Class

### Properties

## int CurrentItem

The item in focus (multi-selection mode).
## 🔒︎ string CurrentItemData

The data of the focused item (multi-selection mode). The data can be used as a text identifier of the item (instead of using the number of the item).
## 🔒︎ string CurrentItemText

The text of the focused item (multi-selection mode).
## 🔒︎ int NumItems

The number of visible items in the tree box. Items that are currently [collapsed](#isItemFolded_int_int) to a parent level are not returned.
## 🔒︎ int NumSelectedItems

The number of selected items in the box (multi-selection mode).
## string Texture

The file name of the image with mini-icons. the texture is a vertical strip of square icons.
## bool MultiSelection

The value indicating if multiple selection of items is enabled. The default is 0.
## bool Editable

The value indicating if item hierarchy can be edited. The default is 0.
## vec4 SelectionColor

The color to be used to highlight the current selection for the widget.
## string StyleTextureSelection

The skin used to highlight the current selection for the widget.
## 🔒︎ int ItemUnderCursor

The item ID in range from 0 to the total number of items, over which the cursor is currently hovering.
## bool NeedSortChildren

The value indicating if sorting of children is enabled. Sorting is performed with the default compare algorithm.
### Members

---

## WidgetTreeBox ( Gui gui )

Constructor. Creates an empty tree box and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new tree box will belong.

## WidgetTreeBox ( )

Constructor. Creates an empty tree box and adds it to the Engine GUI.
## int GetItem ( int num )

Returns the ID of a given item by its number. The IDs are unique, and the numbers simply point at the place in the list of all items.
### Arguments

- *int* **num** - Item ID in range from 0 to the total number of items.

### Return value

Item ID.
## int GetItemChild ( int item , int num )

Returns a child of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **num** - Child number in the list of children in range from 0 to the total number.

### Return value

Child item ID.
## int IsItemChild ( int item , int child )

Checks if a given item is a child of another specified item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

### Return value

**1** if *child* is actually a child of the *item*; otherwise, **0**.
## void SetItemColor ( int item , vec4 color )

Sets a custom color for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *vec4* **color** - Color to set.

## vec4 GetItemColor ( int item )

Returns a color set to a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Color.
## void SetItemData ( int item , string str )

Sets a custom text data for the given item. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *string* **str** - Text data to be set.

## string GetItemData ( int item )

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified ID. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Item text data.
## void SetItemFolded ( int item , int folded )

Expands or collapses an hierarchy of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **folded** - 1 to collapse the item hierarchy, 0 to expand it.

## int IsItemFolded ( int item )

Returns a value indicating if a given item is collapsed.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is collapsed; otherwise, **0**.
## void SetItemHidden ( int item , int hidden )

Sets a value indicating if a given item is hidden.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **hidden** - 1 to hide the item, 0 to show it.

## int IsItemHidden ( int item )

Returns a value indicating if an item is hidden or not.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is hidden; otherwise, **0**.
## void SetItemParent ( int item , int parent )

Sets a parent for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **parent** - Parent item ID. -1 removes the current parent.

## int GetItemParent ( int item )

Returns the parent of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Parent item ID.
## void GetItems ( int[] OUT_items )

Returns all items in the tree box.
### Arguments

- *int[]* **OUT_items** - An array with item IDs. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetItemSelectable ( int item , int selectable )

Sets a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **selectable** - **1** to set the item as selectable, **0** to set it as unselectable.

## int IsItemSelectable ( int item )

Returns a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is selectable; otherwise, **0**.
## void SetItemSelected ( int item , int selected )

Selects or deselects a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **selected** - 1 to select the item, 0 to deselect it.

## int IsItemSelected ( int item )

Returns a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is selected; otherwise, **0**.
## void SetItemText ( int item , string str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *string* **str** - Item text.

## string GetItemText ( int item )

Returns the text of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Item text.
## void SetItemTexture ( int item , int texture )

Sets an icon for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

## int GetItemTexture ( int item )

Returns the icon of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Zero-based ID of the icon (i.e. number of the icon in the icon texture).
## int GetNumItemChildren ( int item )

Returns the number of child items of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Number of child items.
## int GetSelectedItem ( int num )

Returns ID of a selected item (multi-selection mode).
### Arguments

- *int* **num** - Number of an item in the list of selected items.

### Return value

ID of the selected item.
## int AddItem ( string str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *string* **str** - Item text.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture). -1 means that an item has no icon.

### Return value

ID of the added item.
## void AddItemChild ( int item , int child )

Adds a child to a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

## void Clear ( )

Removes all items from the tree box.
## void ClearSelection ( )

Clears list of selected items.
## void RemoveItem ( int item )

Removes a given item from the tree box. Children items will be kept.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

## void RemoveItemChild ( int item , int child )

Removes a child of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

## void ShowItem ( int item )

Scrolls a tree box so that a given item is visible.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

## void SetImage ( Image image )

Sets an image with mini-icons to be used with list items. The image is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetImage ( )

Returns the image with mini-icons, which are used with the list items.
### Return value

Image with mini-icons (the vertical strip of square icons).
## void ClearIcons ( )

Removes all per-slot icon overrides set via **[SetIcon()](../../...md#setIcon_int_cstr_int)** and recalculates the icon cell size, so the items fall back to the icon atlas texture.
## bool SetIcon ( int index , string path )

Assigns a standalone image as the icon for the specified icon slot, overriding the corresponding slot of the treebox's icon atlas (items reference icons via the texture number set for the item). The image may have its own size: the overall icon cell grows to the maximum icon dimensions.
### Arguments

- *int* **index** - Icon slot number (0 or greater) referenced by items via their texture number.
- *string* **path** - Path to the image file.

### Return value

true if the icon is set successfully; otherwise, false (a negative index or the image cannot be loaded).
