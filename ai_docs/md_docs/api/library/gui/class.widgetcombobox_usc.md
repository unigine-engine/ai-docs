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

## void setStyleTextureBorder ( string border )

Sets a new skin used for the widget's border.
### Arguments

- *string* **border** - The skin used for the widget's border

## const char * getStyleTextureBorder () const

Returns the current skin used for the widget's border.
### Return value

Current skin used for the widget's border
## void setStyleTextureBackground ( string background )

Sets a new skin used for the widget's background.
### Arguments

- *string* **background** - The skin used for the widget's background

## const char * getStyleTextureBackground () const

Returns the current skin used for the widget's background.
### Return value

Current skin used for the widget's background
## void setStyleTextureSelection ( string selection )

Sets a new skin used to highlight the current selection for the widget.
### Arguments

- *string* **selection** - The skin used to highlight the current selection for the widget

## const char * getStyleTextureSelection () const

Returns the current skin used to highlight the current selection for the widget.
### Return value

Current skin used to highlight the current selection for the widget
## void setStyleTextureButton ( string button )

Sets a new path to the skin used for buttons.
### Arguments

- *string* **button** - The path to the skin used for buttons

## const char * getStyleTextureButton () const

Returns the current path to the skin used for buttons.
### Return value

Current path to the skin used for buttons
## void setStyleTextureIcon ( string icon )

Sets a new path to the skin used for icons.
### Arguments

- *string* **icon** - The path to the skin used for icons

## const char * getStyleTextureIcon () const

Returns the current path to the skin used for icons.
### Return value

Current path to the skin used for icons
## void setCurrentItem ( int item )

Sets a new number of the currently selected item.
### Arguments

- *int* **item** - The number of the currently selected item

## int getCurrentItem () const

Returns the current number of the currently selected item.
### Return value

Current number of the currently selected item
## int getNumItems () const

Returns the current number of items in the combobox.
### Return value

Current number of items in the combobox
## void setTexture ( string texture )

Sets a new path to the image with mini icons, which are used with combobox items.
### Arguments

- *string* **texture** - The path to the image with mini icons, which are used with combobox items

## const char * getTexture () const

Returns the current path to the image with mini icons, which are used with combobox items.
### Return value

Current path to the image with mini icons, which are used with combobox items
## void setButtonColor ( vec4 color )

Sets a new color for the widget's button.
### Arguments

- *vec4* **color** - The color for the widget's button

## vec4 getButtonColor () const

Returns the current color for the widget's button.
### Return value

Current color for the widget's button
## void setBorderColor ( vec4 color )

Sets a new border color for the widget.
### Arguments

- *vec4* **color** - The border color for the widget

## vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current border color for the widget
## void setSelectionColor ( vec4 color )

Sets a new color used to highlight the current selection for the widget.
### Arguments

- *vec4* **color** - The color used to highlight the current selection for the widget

## vec4 getSelectionColor () const

Returns the current color used to highlight the current selection for the widget.
### Return value

Current color used to highlight the current selection for the widget
## void setListBackgroundColor ( vec4 color )

Sets a new background color used for the widget's list items.
### Arguments

- *vec4* **color** - The background color used for the widget's list items

## vec4 getListBackgroundColor () const

Returns the current background color used for the widget's list items.
### Return value

Current background color used for the widget's list items
## void setMainBackgroundColor ( vec4 color )

Sets a new background color used for the widget's text box.
### Arguments

- *vec4* **color** - The background color used for the widget's text box

## vec4 getMainBackgroundColor () const

Returns the current background color used for the widget's text box.
### Return value

Current background color used for the widget's text box
---

## static WidgetComboBox ( Gui gui )

Constructor. Creates an empty combobox and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new combobox will belong.

## static WidgetComboBox ( )

Constructor. Creates an empty combobox and adds it to the Engine GUI.
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

## int findItemByText ( string str )

Returns the number of the item the text of which is the same as in the argument.
### Arguments

- *string* **str** - Item text.

### Return value

Number of the item with the matching text.
