# Unigine::WidgetIcon Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a toggleable [icon](../../../code/gui/ui/ui_widgets.md#icon) with two states - pressed or not.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/icon.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetIcon Class

### Members

## void setText ( const char * text )

Sets a new floating text placed over the icon.
### Arguments

- *const char ** **text** - The floating text placed over the icon

## const char * getText () const

Returns the current floating text placed over the icon.
### Return value

Current floating text placed over the icon
## void setTextAlign ( int align )

Sets a new alignment flag set for the floating text over the icon. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cpp.md) variables. The default is *ALIGN_CENTER*.
### Arguments

- *int* **align** - The alignment flag set for the floating text over the icon

## int getTextAlign () const

Returns the current alignment flag set for the floating text over the icon. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cpp.md) variables. The default is *ALIGN_CENTER*.
### Return value

Current alignment flag set for the floating text over the icon
## void setTexture ( const char * texture )

Sets a new path to the icon image.
### Arguments

- *const char ** **texture** - The path to the icon image

## const char * getTexture () const

Returns the current path to the icon image.
### Return value

Current path to the icon image
## void setToggled ( bool toggled )

Sets a new value indicating if the icon serving as a toggle button is pressed.
### Arguments

- *bool* **toggled** - true if the toggle icon is pressed, false if it is released

## bool isToggled () const

Returns the current value indicating if the icon serving as a toggle button is pressed.
### Return value

true if the toggle icon is pressed, false if it is released
## void setToggleable ( bool toggleable )

Sets a new value indicating if the icon is a toggle button or a simple button. The default is 0.
### Arguments

- *bool* **toggleable** - true if the icon is a toggle button, false if it is a simple one

## bool isToggleable () const

Returns the current value indicating if the icon is a toggle button or a simple button. The default is 0.
### Return value

true if the icon is a toggle button, false if it is a simple one
---

## static WidgetIconPtr create ( const Ptr < Gui > & gui , const char * str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new icon will belong.
- *const char ** **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## static WidgetIconPtr create ( const char * str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## void setImage ( const Ptr < Image > & image )

Sets an icon image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Returns the icon image.
### Return value

Icon image.
