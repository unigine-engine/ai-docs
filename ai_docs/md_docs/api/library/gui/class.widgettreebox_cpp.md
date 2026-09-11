# Unigine::WidgetTreeBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

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

### Members

## void setCurrentItem ( int item )

Sets a new item in focus (multi-selection mode).
### Arguments

- *int* **item** - The item ID.

## int getCurrentItem () const

Returns the current item in focus (multi-selection mode).
### Return value

Current item ID.
## const char * getCurrentItemData () const

Returns the current data of the focused item (multi-selection mode). The data can be used as a text identifier of the item (instead of using the number of the item).
### Return value

Current item data.
## const char * getCurrentItemText () const

Returns the current text of the focused item (multi-selection mode).
### Return value

Current item text.
## int getNumItems () const

Returns the current number of visible items in the tree box. Items that are currently [collapsed](#isItemFolded_int_int) to a parent level are not returned.
### Return value

Current number of items.
## int getNumSelectedItems () const

Returns the current number of selected items in the box (multi-selection mode).
### Return value

Current number of selected items.
## void setTexture ( const char * texture )

Sets a new file name of the image with mini-icons. the texture is a vertical strip of square icons.
### Arguments

- *const char ** **texture** - The path to the texture file.

## const char * getTexture () const

Returns the current file name of the image with mini-icons. the texture is a vertical strip of square icons.
### Return value

Current path to the texture file.
## void setMultiSelection ( bool selection )

Sets a new value indicating if multiple selection of items is enabled. The default is 0.
### Arguments

- *bool* **selection** - Set **true** to enable multiple selection of items; **false** - to disable it.

## bool isMultiSelection () const

Returns the current value indicating if multiple selection of items is enabled. The default is 0.
### Return value

**true** if multiple selection of items is enabled ; otherwise **false**.
## void setEditable ( bool editable )

Sets a new value indicating if item hierarchy can be edited. The default is 0.
### Arguments

- *bool* **editable** - Set **true** to enable hierarchy can be edited; **false** - to disable it.

## bool isEditable () const

Returns the current value indicating if item hierarchy can be edited. The default is 0.
### Return value

**true** if hierarchy can be edited; otherwise **false**.
## void setSelectionColor ( const Math:: vec4 & color )

Sets a new color to be used to highlight the current selection for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getSelectionColor () const

Returns the current color to be used to highlight the current selection for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setStyleTextureSelection ( const char * selection )

Sets a new skin used to highlight the current selection for the widget.
### Arguments

- *const char ** **selection** - The Path to a texture file.

## const char * getStyleTextureSelection () const

Returns the current skin used to highlight the current selection for the widget.
### Return value

Current Path to a texture file.
## int getItemUnderCursor () const

Returns the current item ID in range from 0 to the total number of items, over which the cursor is currently hovering.
### Return value

Current item ID.
## void setNeedSortChildren ( bool children )

Sets a new value indicating if sorting of children is enabled. Sorting is performed with the default compare algorithm.
### Arguments

- *bool* **children** - Set **true** to enable sorting of children; **false** - to disable it.

## bool isNeedSortChildren () const

Returns the current value indicating if sorting of children is enabled. Sorting is performed with the default compare algorithm.
### Return value

**true** if sorting of children is enabled ; otherwise **false**.
---

## static WidgetTreeBoxPtr create ( const Ptr < Gui > & gui )

Constructor. Creates an empty tree box and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new tree box will belong.

## static WidgetTreeBoxPtr create ( )

Constructor. Creates an empty tree box and adds it to the Engine GUI.
## int getItem ( int num ) const

Returns the ID of a given item by its number. The IDs are unique, and the numbers simply point at the place in the list of all items.
### Arguments

- *int* **num** - Item ID in range from 0 to the total number of items.

### Return value

Item ID.
## int getItemChild ( int item , int num ) const

Returns a child of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **num** - Child number in the list of children in range from 0 to the total number.

### Return value

Child item ID.
## int isItemChild ( int item , int child ) const

Checks if a given item is a child of another specified item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

### Return value

**1** if *child* is actually a child of the *item*; otherwise, **0**.
## void setItemColor ( int item , const Math:: vec4 & color )

Sets a custom color for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to set.

## Math:: vec4 getItemColor ( int item ) const

Returns a color set to a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Color.
## void setItemData ( int item , const char * str )

Sets a custom text data for the given item. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *const char ** **str** - Text data to be set.

## const char * getItemData ( int item ) const

Returns the [text data](#setItemData_int_cstr_void) of the item with the specified ID. The data can be used as a text identifier of the item (instead of using the item number).
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Item text data.
## void setItemFolded ( int item , int folded )

Expands or collapses an hierarchy of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **folded** - 1 to collapse the item hierarchy, 0 to expand it.

## int isItemFolded ( int item ) const

Returns a value indicating if a given item is collapsed.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is collapsed; otherwise, **0**.
## void setItemHidden ( int item , int hidden )

Sets a value indicating if a given item is hidden.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **hidden** - 1 to hide the item, 0 to show it.

## int isItemHidden ( int item ) const

Returns a value indicating if an item is hidden or not.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is hidden; otherwise, **0**.
## void setItemParent ( int item , int parent )

Sets a parent for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **parent** - Parent item ID. -1 removes the current parent.

## int getItemParent ( int item ) const

Returns the parent of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Parent item ID.
## void getItems ( Vector <int> & OUT_items ) const

Returns all items in the tree box.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_items** - An array with item IDs. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setItemSelectable ( int item , int selectable )

Sets a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **selectable** - **1** to set the item as selectable, **0** to set it as unselectable.

## int isItemSelectable ( int item ) const

Returns a value indicating if a given item can be selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is selectable; otherwise, **0**.
## void setItemSelected ( int item , int selected )

Selects or deselects a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **selected** - 1 to select the item, 0 to deselect it.

## int isItemSelected ( int item ) const

Returns a value indicating if a given item is selected.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

**1** if the item is selected; otherwise, **0**.
## void setItemText ( int item , const char * str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *const char ** **str** - Item text.

## const char * getItemText ( int item ) const

Returns the text of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Item text.
## void setItemTexture ( int item , int texture )

Sets an icon for a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture).

## int getItemTexture ( int item ) const

Returns the icon of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Zero-based ID of the icon (i.e. number of the icon in the icon texture).
## int getNumItemChildren ( int item ) const

Returns the number of child items of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

### Return value

Number of child items.
## int getSelectedItem ( int num ) const

Returns ID of a selected item (multi-selection mode).
### Arguments

- *int* **num** - Number of an item in the list of selected items.

### Return value

ID of the selected item.
## int addItem ( const char * str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *const char ** **str** - Item text.
- *int* **texture** - Zero-based ID of the icon (i.e. number of the icon in the icon texture). -1 means that an item has no icon.

### Return value

ID of the added item.
## void addItemChild ( int item , int child )

Adds a child to a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

## void clear ( )

Removes all items from the tree box.
## void clearSelection ( )

Clears list of selected items.
## void removeItem ( int item )

Removes a given item from the tree box. Children items will be kept.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

## void removeItemChild ( int item , int child )

Removes a child of a given item.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.
- *int* **child** - Child item ID.

## void showItem ( int item )

Scrolls a tree box so that a given item is visible.
### Arguments

- *int* **item** - Item ID in range from 0 to the total number of items.

## void setImage ( const Ptr < Image > & image )

Sets an image with mini-icons to be used with list items. The image is a vertical strip of square icons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Returns the image with mini-icons, which are used with the list items.
### Return value

Image with mini-icons (the vertical strip of square icons).
## void clearIcons ( )

Removes all per-slot icon overrides set via **[setIcon()](../../...md#setIcon_int_cstr_int)** and recalculates the icon cell size, so the items fall back to the icon atlas texture.
## bool setIcon ( int index , const char * path )

Assigns a standalone image as the icon for the specified icon slot, overriding the corresponding slot of the treebox's icon atlas (items reference icons via the texture number set for the item). The image may have its own size: the overall icon cell grows to the maximum icon dimensions.
### Arguments

- *int* **index** - Icon slot number (0 or greater) referenced by items via their texture number.
- *const char ** **path** - Path to the image file.

### Return value

true if the icon is set successfully; otherwise, false (a negative index or the image cannot be loaded).
