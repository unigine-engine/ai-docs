# Unigine::WidgetTabBox Class (CS)

**Inherits from:** Widget


This class creates a [box with several tabs](../../../code/gui/ui/ui_containers.md#tabbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/tabbox.png)


## WidgetTabBox Class

### Properties

## int CurrentTab

The tab number.
## 🔒︎ int NumTabs

The total number of tabs in the box.
## string Texture

The path to the tab icons atlas texture. This atlas is a vertical strip of square icons.
## 🔒︎ int PaddingBottom

The bottom padding for the widget content.
## 🔒︎ int PaddingTop

The top padding for the widget content.
## 🔒︎ int PaddingRight

The right-side padding for the widget content.
## 🔒︎ int PaddingLeft

The left-side padding for the widget content.
## 🔒︎ int SpaceY

The vertical space between the widgets in the box and between them and the box border.
## 🔒︎ int SpaceX

The horizontal space between the widgets in the box and between them and the box border.
## vec4 BorderColor

The border color for the widget.
## vec4 ButtonColor

The color for the widget's button.
### Members

---

## WidgetTabBox ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates a tabbed box with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## WidgetTabBox ( int x = 0 , int y = 0 )

Constructor. Creates a tabbed box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## string GetCurrentTabData ( )

Returns the data of the current tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Return value

Tab data.
## string GetCurrentTabText ( )

Returns the title of the current tab.
### Return value

Tab title.
## void SetImage ( Image image )

Sets a tab icons atlas image. This atlas is a vertical strip of square icons.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Tabs atlas.

## Image GetImage ( )

Returns the tab icons atlas image. This atlas is a vertical strip of square icons.
### Return value

Tabs atlas.
## void SetPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void SetSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is provided, 0 will be used instead.

## void SetTabData ( int num , string str )

Sets the data for the given tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *string* **str** - Data to set.

## string GetTabData ( int num )

Returns the data of a given tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Tab data.
## void SetTabHidden ( int num , bool hidden )

Sets a value indicating that a specified tab should not be rendered visible. By default all widget tabs are visible.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *bool* **hidden** - true for the tab to be invisible; otherwise, false.

## bool IsTabHidden ( int num )

Returns a value indicating if the specified tab is invisible.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

true if the specified tab is invisible; otherwise, false.
## void SetTabText ( int num , string str )

Sets a title for the current tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *string* **str** - Tab title.

## string GetTabText ( int num )

Returns the title of a given tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Tab title.
## void SetTabTexture ( int num , int texture )

Sets an icon for the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *int* **texture** - Zero-based ID of the icon (icon number in the atlas column). -1 specifies that a tab has no icon.

## int GetTabTexture ( int num )

Returns the icon of the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Zero-based ID of the icon (icon number in the atlas column). -1 specifies that a tab has no icon.
## void SetTabToolTip ( int num , string str )

Sets a tooltip for the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *string* **str** - Tooltip to display.

## string GetTabToolTip ( int num )

Returns the tooltip of the given tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Displayed tooltip.
## int AddTab ( string str , int texture = -1 )

Adds a new tab with a given title and icon to the box.
### Arguments

- *string* **str** - Tab title.
- *int* **texture** - Zero-based ID of the icon (icon number in the atlas column). -1 means that a tab has no icon.

### Return value

Number of the added tab.
## void Clear ( )

Removes all tabs from the box.
## void RemoveTab ( int num )

Removes a given tab from the box.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
