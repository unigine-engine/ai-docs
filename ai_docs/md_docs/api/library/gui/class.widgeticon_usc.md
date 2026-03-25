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
## void setText ( string text )

Sets the floating text over the icon.
### Arguments

- *string* **text** - Floating text.

## string getText ( )

Returns the current floating text set to be over the icon.
### Return value

Floating text.
## void setTextAlign ( int align )

Sets the alignment flag for the floating text over the icon. The default is *GUI_ALIGN_CENTER*.
### Arguments

- *int* **align** - Alignment flag (see *GUI_ALIGN_** variables).

## int getTextAlign ( )

Returns the current alignment flag set for the floating text over the icon.
### Return value

Alignment flag (one of the *GUI_ALIGN_** variables).
## void setTexture ( string texture )

Sets a texture to be used as the icon image.
### Arguments

- *string* **texture** - Path to a texture file.

## string getTexture ( )

Returns path to the icon image.
### Return value

Path to the icon image.
## void setToggleable ( int toggleable )

Sets a value indicating if the icon is a toggle button or a simple button.
### Arguments

- *int* **toggleable** - Positive number to make the icon a toggle button, 0 to make it a simple button.

## int isToggleable ( )

Returns a value indicating if the icon is a toggle button or a simple button.
### Return value

Positive number if the icon is a toggle button; otherwise, 0.
## void setToggled ( int toggled )

Sets a state of the icon as a toggle button.
### Arguments

- *int* **toggled** - Positive number to press the button, 0 to release it.

## int isToggled ( )

Returns a value indicating if the icon serving as a toggle button is pressed.
### Return value

**1** if the button is pressed; otherwise, **0**.
