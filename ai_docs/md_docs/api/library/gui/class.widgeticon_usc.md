# Unigine::WidgetIcon Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a toggleable [icon](../../../code/gui/ui/ui_widgets.md#icon) with two states - pressed or not.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/icon.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetIcon Class

### Members

## void setText ( string text )

Sets a new floating text placed over the icon.
### Arguments

- *string* **text** - The floating text placed over the icon

## const char * getText () const

Returns the current floating text placed over the icon.
### Return value

Current floating text placed over the icon
## void setTextAlign ( int align )

Sets a new alignment flag set for the floating text over the icon. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_usc.md) variables. The default is *ALIGN_CENTER*.
### Arguments

- *int* **align** - The alignment flag set for the floating text over the icon

## int getTextAlign () const

Returns the current alignment flag set for the floating text over the icon. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_usc.md) variables. The default is *ALIGN_CENTER*.
### Return value

Current alignment flag set for the floating text over the icon
## void setTexture ( string texture )

Sets a new path to the icon image.
### Arguments

- *string* **texture** - The path to the icon image

## const char * getTexture () const

Returns the current path to the icon image.
### Return value

Current path to the icon image
## void setToggled ( int toggled )

Sets a new value indicating if the icon serving as a toggle button is pressed.
### Arguments

- *int* **toggled** - The true if the toggle icon is pressed, false if it is released

## int isToggled () const

Returns the current value indicating if the icon serving as a toggle button is pressed.
### Return value

Current true if the toggle icon is pressed, false if it is released
## void setToggleable ( int toggleable )

Sets a new value indicating if the icon is a toggle button or a simple button. The default is 0.
### Arguments

- *int* **toggleable** - The true if the icon is a toggle button, false if it is a simple one

## int isToggleable () const

Returns the current value indicating if the icon is a toggle button or a simple button. The default is 0.
### Return value

Current true if the icon is a toggle button, false if it is a simple one
---

## static WidgetIcon ( Gui gui , string str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new icon will belong.
- *string* **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## static WidgetIcon ( string str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the Engine GUI.
### Arguments

- *string* **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## void setImage ( Image image )

Sets an icon image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getImage ( )

Returns the icon image.
### Return value

Icon image.
