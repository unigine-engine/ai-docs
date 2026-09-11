# Unigine::WidgetComboBox Class (CS)

**Inherits from:** Widget


This class creates a [combo box](../../../code/gui/ui/ui_widgets.md#combobox).


The object of this class looks as follows:


![Combo box widget](../../../code/gui/ui/widgets/combobox.png)


#### See Also


- C++ sample
- C# Component sample


### Example


The following code illustrates how to create a combobox widget and set its parameters.


```csharp
/* .. */

// event handler function
void onComboBoxChanged()
{
	/* .. */

}

/* .. */

void Init()
{
	// getting a pointer to the system GUI
	Gui gui = Gui.GetCurrent();

	// creating a combobox widget
	WidgetComboBox widget_combo = new WidgetComboBox(gui);

	// adding items to the combobox
	widget_combo.AddItem("----ALL-----");
	widget_combo.AddItem("Item 1");
	widget_combo.AddItem("Item 2");
	widget_combo.AddItem("Item 3");

	// setting a tooltip
	widget_combo.SetToolTip("This is a combo box");

	// rearranging combobox size
	widget_combo.Arrange();

	// setting combobox position
	widget_combo.SetPosition(10, 10);

	// setting the first item as currently selected one
	widget_combo.CurrentItem = 0;

	// setting onComboBoxChanged function to handle CHANGED event
	widget_combo.EventChanged.Connect(onComboBoxChanged);

	// adding created combobox widget to the system GUI
	gui.AddChild(widget_combo, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);

}


```


## WidgetComboBox Class

### Properties

## string StyleTextureBorder

The skin used for the widget's border.
## string StyleTextureBackground

The skin used for the widget's background.
## string StyleTextureSelection

The skin used to highlight the current selection for the widget.
## string StyleTextureButton

The path to the skin used for buttons.
## string StyleTextureIcon

The path to the skin used for icons.
## int CurrentItem

The number of the currently selected item.
## 🔒︎ int NumItems

The number of items in the combobox.
## string Texture

The path to the image with mini icons, which are used with combobox items.
## vec4 ButtonColor

The color for the widget's button.
## vec4 BorderColor

The border color for the widget.
## vec4 SelectionColor

The color used to highlight the current selection for the widget.
## vec4 ListBackgroundColor

The background color used for the widget's list items.
## vec4 MainBackgroundColor

The background color used for the widget's text box.
### Members

---

## WidgetComboBox ( Gui gui )

Constructor. Creates an empty combobox and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new combobox will belong.

## WidgetComboBox ( )

Constructor. Creates an empty combobox and adds it to the Engine GUI.
## string GetCurrentItemData ( )

Returns the [text data](#setItemData_int_cstr_void) of the currently selected item. The data can be used as a text identifier of the item (instead of using the item number).
### Return value

Item text data.
## string GetCurrentItemText ( )

Returns a text value of the currently selected item.
### Return value

Item text.
## void SetImage ( Image image )

Sets an image with mini icons to be used with items. The image is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetImage ( )

Returns the image with mini icons, which are used for the combobox items.
### Return value

Image with mini icons.
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

Item text data.
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
- *int* **texture** - Zero-based ID of the icon.

## int GetItemTexture ( int item )

Returns the icon of a given item.
### Arguments

- *int* **item** - Item number.

### Return value

Zero-based ID of the icon.
## int AddItem ( string str , int texture = -1 )

Adds a new item with a given text and an icon.
### Arguments

- *string* **str** - Item text.
- *int* **texture** - Zero-based ID of the icon.

### Return value

Number of the added item.
## void Clear ( )

Removes all items from the combobox.
## void RemoveItem ( int num )

Removes a given item from the combobox.
### Arguments

- *int* **num** - Item number.

## int FindItemByText ( string str )

Returns the number of the item the text of which is the same as in the argument.
### Arguments

- *string* **str** - Item text.

### Return value

Number of the item with the matching text.
