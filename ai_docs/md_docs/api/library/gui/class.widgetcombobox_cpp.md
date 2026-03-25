# Unigine::WidgetComboBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [combo box](../../../code/gui/ui/ui_widgets.md#combobox).


The object of this class looks as follows:


![Combo box widget](../../../code/gui/ui/widgets/combobox.png)


#### See Also


- C++ sample
- C# Component sample


### Example


The following code illustrates how to create a combobox widget and set its parameters.


```cpp
#include "AppWorldLogic.h"
#include <UnigineGui.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

/* .. */

// event handler function
int onComboBoxChanged()
{
	/* .. */

	return 1;
}

/* .. */

int AppWorldLogic::init()
{
	// getting a pointer to the system GUI
	GuiPtr gui = Gui::getCurrent();

	// creating a combobox widget
	WidgetComboBoxPtr widget_combo = WidgetComboBox::create(gui);

	// adding items to the combobox
	widget_combo->addItem("----ALL-----");
	widget_combo->addItem("Item 1");
	widget_combo->addItem("Item 2");
	widget_combo->addItem("Item 3");

	// setting a tooltip
	widget_combo->setToolTip("This is a combo box");

	// rearranging combobox size
	widget_combo->arrange();

	// setting combobox position
	widget_combo->setPosition(10, 10);

	// setting the first item as currently selected one
	widget_combo->setCurrentItem(0);

	// setting onComboBoxChanged function to handle CHANGED event
	widget_combo->getEventChanged().connect(econnections, onComboBoxChanged);

	// adding created combobox widget to the system GUI
	gui->addChild(widget_combo, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

	return 1;
}

int AppWorldLogic::shutdown()
{
	// removing all event subscriptions
	econnections.disconnectAll();

	return 1;
}


```


## WidgetComboBox Class

### Members

---

## static WidgetComboBoxPtr create ( const Ptr < Gui > & gui )

Constructor. Creates an empty combobox and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new combobox will belong.

## static WidgetComboBoxPtr create ( )

Constructor. Creates an empty combobox and adds it to the Engine GUI.
## void setCurrentItem ( int item )

Sets a given item as selected.
### Arguments

- *int* **item** - Item number.

## int getCurrentItem ( ) const

Returns the currently selected item.
### Return value

Item number.
## const char * getCurrentItemData ( ) const

Returns the [text data](#setItemData_int_cstr_void) of the currently selected item. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## const char * getCurrentItemText ( ) const

Returns a text value of the currently selected item.
### Return value

Item text.
## void setImage ( const Ptr < Image > & image )

Sets an image with mini icons to be used with items. The image is a vertical strip of square icons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Returns the image with mini icons, which are used for the combobox items.
### Return value

Image with mini icons.
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

Item text data.
## void setItemText ( int item , const char * str )

Sets a text for a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.
- *const char ** **str** - Item text.

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
- *int* **texture** - Zero-based ID of the icon.

## int getItemTexture ( int item ) const

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number in range from 0 to the total number of items.

### Return value

Zero-based ID of the icon.
## int getNumItems ( ) const

Returns the number of items in the combobox.
### Return value

Number of items.
## void setTexture ( const char * texture )

Sets a texture with mini icons to be used with items. The texture is a vertical strip of square icons.
### Arguments

- *const char ** **texture** - Path to a texture file.

## const char * getTexture ( ) const

Returns path to the image with mini icons, which are used with combobox items.
### Return value

Path to the texture file.
## int addItem ( const char * str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *const char ** **str** - Item text.
- *int* **texture** - Zero-based ID of the icon.

### Return value

Number of the added item.
## void clear ( )

Removes all items from the combobox.
## void removeItem ( int num )

Removes a given item from the combobox.
### Arguments

- *int* **num** - Item number in range from 0 to the total number of items.

## void setMainBackgroundColor ( const Math:: vec4 & color )

Sets the background color to be used for the widget's text box.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getMainBackgroundColor ( ) const

Returns the current background color used for the widget's text box.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setListBackgroundColor ( const Math:: vec4 & color )

Sets the background color to be used for the widget's list items.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getListBackgroundColor ( ) const

Returns the current background color used for the widget's list items.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setSelectionColor ( const Math:: vec4 & color )

Sets the color to be used to highlight the current selection for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getSelectionColor ( ) const

Returns the current color used to highlight the current selection for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setBorderColor ( const Math:: vec4 & color )

Sets the border color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBorderColor ( ) const

Returns the current border color for the widget.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setButtonColor ( const Math:: vec4 & color )

Sets the color for the widget's button.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getButtonColor ( ) const

Returns the current color for the widget's button.
### Return value

Four-component vector specifying the color in the RGBA format.
## int findItemByText ( const char * str ) const

Returns the number of the item the text of which is the same as in the argument.
### Arguments

- *const char ** **str** - Item text.

### Return value

Number of the item with the matching text.
## void setStyleTextureIcon ( const char * icon )

Sets a skin to be used for icons.
### Arguments

- *const char ** **icon** - Path to a texture file.

## const char * getStyleTextureIcon ( ) const

Returns the path to the skin used for icons.
### Return value

Path to the texture file.
## void setStyleTextureButton ( const char * button )

Sets a skin to be used for buttons.
### Arguments

- *const char ** **button** - Path to a texture file.

## const char * getStyleTextureButton ( ) const

Returns the path to the skin used for buttons.
### Return value

Path to a texture file.
## void setStyleTextureSelection ( const char * selection )

Sets a skin used to highlight the current selection for the widget.
### Arguments

- *const char ** **selection** - Path to a texture file.

## const char * getStyleTextureSelection ( ) const

Returns the skin used to highlight the current selection for the widget.
### Return value

Path to a texture file.
## void setStyleTextureBackground ( const char * background )

Sets a skin to be used for the widget's background.
### Arguments

- *const char ** **background** - Path to a texture file.

## const char * getStyleTextureBackground ( ) const

Returns the skin used for the widget's background.
### Return value

Path to a texture file.
## void setStyleTextureBorder ( const char * border )

Sets a skin to be used for the widget's border.
### Arguments

- *const char ** **border** - Path to a texture file.

## const char * getStyleTextureBorder ( ) const

Returns the skin used for the widget's border.
### Return value

Path to a texture file.
