# Unigine::WidgetComboBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [combo box](../../../code/gui/ui/ui_widgets.md#combobox).


The object of this class looks as follows:


![Combo box widget](../../../code/gui/ui/widgets/combobox.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetComboBox Class

### Members

---

## static WidgetComboBox ( Gui gui )

Constructor. Creates an empty combobox and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new combobox will belong.

## static WidgetComboBox ( )

Constructor. Creates an empty combobox and adds it to the Engine GUI.
## void setCurrentItem ( int item )

Selects a given item.
### Arguments

- *int* **item** - Item number.

## int getCurrentItem ( )

Returns the currently selected item.
### Return value

Item number.
## string getCurrentItemData ( )

Returns the [text data](#setItemData_int_cstr_void) of the currently selected item. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## string getCurrentItemText ( )

Returns a text value of the currently selected item.
### Return value

Item text.
## void setImage ( Image image )

Sets an image with mini icons to be used with items. The image is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getImage ( )

Returns the image with mini icons, which are used for the combobox items.
### Return value

Image with mini icons.
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

Item text data.
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
- *int* **texture** - Zero-based ID of the icon.

## int getItemTexture ( int item )

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Zero-based ID of the icon.
## int getNumItems ( )

Returns the number of items in the combobox.
### Return value

Number of items.
## void setTexture ( string texture )

Sets a texture with mini icons to be used with items. The texture is a vertical strip of square icons.
### Arguments

- *string* **texture** - Path to a texture file.

## string getTexture ( )

Returns file name of the image with mini icons.
### Return value

Path to the texture file.
## int addItem ( string str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *string* **str** - Item text.
- *int* **texture** - Zero-based ID of the icon.

### Return value

Number of the added item.
## void clear ( )

Removes all items from the combobox.
## void removeItem ( int num )

Removes a given item from the combobox.
### Arguments

- *int* **num** - Item number.

## void setMainBackgroundColor ( vec4 color )

Sets the background color to be used for the widget's text box.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getMainBackgroundColor ( )

Returns the current background color used for the widget's text box.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setListBackgroundColor ( vec4 color )

Sets the background color to be used for the widget's list items.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getListBackgroundColor ( )

Returns the current background color used for the widget's list items.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setSelectionColor ( vec4 color )

Sets the color to be used to highlight the current selection for the widget.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getSelectionColor ( )

Returns the current color used to highlight the current selection for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBorderColor ( vec4 color )

Sets the border color for the widget.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getBorderColor ( )

Returns the current border color for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setButtonColor ( vec4 color )

Sets the color for the widget's button.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getButtonColor ( )

Returns the current color for the widget's button.
### Return value

Four-component vector specifying the color in the RGBA format.
## int findItemByText ( string str )

Returns the number of the item the text of which is the same as in the argument.
### Arguments

- *string* **str** - Item text.

### Return value

Number of the item with the matching text.
## void setStyleTextureIcon ( string icon )

Sets a skin to be used for icons.
### Arguments

- *string* **icon** - Path to a texture file.

## string getStyleTextureIcon ( )

Returns the path to the skin used for icons.
### Return value

Path to the texture file.
## void setStyleTextureButton ( string button )

Sets a skin to be used for buttons.
### Arguments

- *string* **button** - Path to a texture file.

## string getStyleTextureButton ( )

Returns the path to the skin used for buttons.
### Return value

Path to a texture file.
## void setStyleTextureSelection ( string selection )

Sets a skin used to highlight the current selection for the widget.
### Arguments

- *string* **selection** - Path to a texture file.

## string getStyleTextureSelection ( )

Returns the skin used to highlight the current selection for the widget.
### Return value

Path to a texture file.
## void setStyleTextureBackground ( string background )

Sets a skin to be used for the widget's background.
### Arguments

- *string* **background** - Path to a texture file.

## string getStyleTextureBackground ( )

Returns the skin used for the widget's background.
### Return value

Path to a texture file.
## void setStyleTextureBorder ( string border )

Sets a skin to be used for the widget's border.
### Arguments

- *string* **border** - Path to a texture file.

## string getStyleTextureBorder ( )

Returns the skin used for the widget's border.
### Return value

Path to a texture file.
