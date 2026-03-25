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
## void setText ( const char * text )

Sets the floating text over the icon.
### Arguments

- *const char ** **text** - Floating text.

## const char * getText ( ) const

Returns the current floating text set to be over the icon.
### Return value

Floating text.
## void setTextAlign ( int align )

Sets the alignment flag for the floating text over the icon. The default is ALIGN_CENTER.
### Arguments

- *int* **align** - Alignment flag: one of the Gui Enumeration with ALIGN_* prefixes.

## int getTextAlign ( ) const

Returns the current alignment flag set for the floating text over the icon.
### Return value

Alignment flag: one of the Gui Enumeration with ALIGN_* prefixes.
## void setTexture ( const char * texture )

Sets a texture to be used as the icon image.
### Arguments

- *const char ** **texture** - to a texture file.

## const char * getTexture ( ) const

Returns path to the icon image.
### Return value

Path to a texture file.
## void setToggleable ( bool toggleable )

Sets a value indicating if the icon is a toggle button or a simple button. The default is 0.
### Arguments

- *bool* **toggleable** - Positive number to make the icon a toggle button, 0 to make it a simple button.

## bool isToggleable ( ) const

Returns a value indicating if the icon is a toggle button or a simple button. The default is 0.
### Return value

Positive number if the icon is a toggle button; otherwise, 0.
## void setToggled ( bool toggled )

Sets a state of the icon as a toggle button.
### Arguments

- *bool* **toggled** - Positive number to press the button, 0 to release it.

## bool isToggled ( ) const

Returns a value indicating if the icon serving as a toggle button is pressed.
### Return value

Returns 1 if the button is pressed; otherwise, 0.
