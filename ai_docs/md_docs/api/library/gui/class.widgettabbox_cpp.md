# Unigine::WidgetTabBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [box with several tabs](../../../code/gui/ui/ui_containers.md#tabbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/tabbox.png)


## WidgetTabBox Class

### Members

## void setCurrentTab ( int tab )

Sets a new tab number.
### Arguments

- *int* **tab** - The tab number in range from 0 to the total number of tabs.

## int getCurrentTab () const

Returns the current tab number.
### Return value

Current tab number in range from 0 to the total number of tabs.
## int getNumTabs () const

Returns the current total number of tabs in the box.
### Return value

Current total number of tabs in the box.
## void setTexture ( const char * texture )

Sets a new path to the tab icons atlas texture. This atlas is a vertical strip of square icons.
### Arguments

- *const char ** **texture** - The path to the atlas texture.

## const char * getTexture () const

Returns the current path to the tab icons atlas texture. This atlas is a vertical strip of square icons.
### Return value

Current path to the atlas texture.
## int getPaddingBottom () const

Returns the current bottom padding for the widget content.
### Return value

Current bottom padding in pixels.
## int getPaddingTop () const

Returns the current top padding for the widget content.
### Return value

Current top padding in pixels.
## int getPaddingRight () const

Returns the current right-side padding for the widget content.
### Return value

Current right-side padding in pixels.
## int getPaddingLeft () const

Returns the current left-side padding for the widget content.
### Return value

Current left-side padding in pixels.
## int getSpaceY () const

Returns the current vertical space between the widgets in the box and between them and the box border.
### Return value

Current vertical space.
## int getSpaceX () const

Returns the current horizontal space between the widgets in the box and between them and the box border.
### Return value

Current horizontal space.
## void setBorderColor ( const Math:: vec4 & color )

Sets a new border color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setButtonColor ( const Math:: vec4 & color )

Sets a new color for the widget's button.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getButtonColor () const

Returns the current color for the widget's button.
### Return value

Current four-component vector specifying the color in the RGBA format.
---

## static WidgetTabBoxPtr create ( const Ptr < Gui > & gui , int x = 0 , int y = 0 )

Constructor. Creates a tabbed box with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## static WidgetTabBoxPtr create ( int x = 0 , int y = 0 )

Constructor. Creates a tabbed box with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## const char * getCurrentTabData ( ) const

Returns the data of the current tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Return value

Tab data.
## const char * getCurrentTabText ( ) const

Returns the title of the current tab.
### Return value

Tab title.
## void setImage ( const Ptr < Image > & image )

Sets a tab icons atlas image. This atlas is a vertical strip of square icons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Tabs atlas.

## Ptr < Image > getImage ( ) const

Returns the tab icons atlas image. This atlas is a vertical strip of square icons.
### Return value

Tabs atlas.
## void setPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void setSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is provided, 0 will be used instead.

## void setTabData ( int num , const char * str )

Sets the data for the given tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *const char ** **str** - Data to set.

## const char * getTabData ( int num ) const

Returns the data of a given tab. The data can be used as a text identifier of the item (instead of using the number of the item).
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Tab data.
## void setTabHidden ( int num , bool hidden )

Sets a value indicating that a specified tab should not be rendered visible. By default all widget tabs are visible.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *bool* **hidden** - true for the tab to be invisible; otherwise, false.

## bool isTabHidden ( int num ) const

Returns a value indicating if the specified tab is invisible.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

true if the specified tab is invisible; otherwise, false.
## void setTabText ( int num , const char * str )

Sets a title for the current tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *const char ** **str** - Tab title.

## const char * getTabText ( int num ) const

Returns the title of a given tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Tab title.
## void setTabTexture ( int num , int texture )

Sets an icon for the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *int* **texture** - Zero-based ID of the icon (icon number in the atlas column). -1 specifies that a tab has no icon.

## int getTabTexture ( int num ) const

Returns the icon of the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Zero-based ID of the icon (icon number in the atlas column). -1 specifies that a tab has no icon.
## void setTabToolTip ( int num , const char * str )

Sets a tooltip for the specified tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
- *const char ** **str** - Tooltip to display.

## const char * getTabToolTip ( int num ) const

Returns the tooltip of the given tab.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.

### Return value

Displayed tooltip.
## int addTab ( const char * str , int texture = -1 )

Adds a new tab with a given title and icon to the box.
### Arguments

- *const char ** **str** - Tab title.
- *int* **texture** - Zero-based ID of the icon (icon number in the atlas column). -1 means that a tab has no icon.

### Return value

Number of the added tab.
## void clear ( )

Removes all tabs from the box.
## void removeTab ( int num )

Removes a given tab from the box.
### Arguments

- *int* **num** - Tab number in range from 0 to the total number of tabs.
