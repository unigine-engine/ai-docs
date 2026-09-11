# Unigine::WidgetButton Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


Interface for widget button handling.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/button.png)


Here is an example of two buttons. Button1 has a background and image, Button2 is without them:


![](../../../code/gui/ui/examples/button.png)


> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture/image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cpp.md)* instead.


#### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


### Example


The following code illustrates how to create a button widget and set its parameters.


```cpp
#include <UnigineWidgets.h>
#include <UnigineUserInterface.h>
using namespace Unigine;

/* .. */

// event handler function
int onButtonClicked()
{
	/* .. */

	return 1;
}

/* .. */

// getting a pointer to the system GUI
GuiPtr gui = Gui::getCurrent();

// creating a button widget and setting its caption
WidgetButtonPtr widget_button = WidgetButton::create(gui, "Delete");

// setting a tooltip
widget_button->setToolTip("Delete object(s)");

// rearranging button size
widget_button->arrange();

// setting button position
widget_button->setPosition(10, 10);

// setting onButtonClicked function to handle CLICKED event
widget_button->getEventClicked().connect(onButtonClicked);

// adding created button widget to the system GUI
gui->addChild(widget_button, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

```


## WidgetButton Class

### Members

## void setStyleTexture ( const char * texture )

Sets a new path to the button skin texture.
### Arguments

- *const char ** **texture** - The path to the button skin texture

## const char * getStyleTexture () const

Returns the current path to the button skin texture.
### Return value

Current path to the button skin texture
## void setText ( const char * text )

Sets a new button text label.
### Arguments

- *const char ** **text** - The button text label

## const char * getText () const

Returns the current button text label.
### Return value

Current button text label
## void setTextAlign ( int align )

Sets a new alignment of the button label. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cpp.md) variables.
### Arguments

- *int* **align** - The alignment of the button label

## int getTextAlign () const

Returns the current alignment of the button label. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cpp.md) variables.
### Return value

Current alignment of the button label
## void setTexture ( const char * texture )

Sets a new path to the button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cpp.md)* instead.

### Arguments

- *const char ** **texture** - The path to the button image texture

## const char * getTexture () const

Returns the current path to the button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cpp.md)* instead.

### Return value

Current path to the button image texture
## void setButtonColor ( const Math:: vec4 & color )

Sets a new color for the button.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color for the button, as a four-component RGBA vector

## Math:: vec4 getButtonColor () const

Returns the current color for the button.
### Return value

Current color for the button, as a four-component RGBA vector
## void setToggled ( bool toggled )

Sets a new value indicating if the toggle button is pressed.
### Arguments

- *bool* **toggled** - true if the toggle button is pressed, false if it is released

## bool isToggled () const

Returns the current value indicating if the toggle button is pressed.
### Return value

true if the toggle button is pressed, false if it is released
## void setToggleable ( bool toggleable )

Sets a new value indicating if the button is a toggle button or a simple one. The default is 0.
### Arguments

- *bool* **toggleable** - true if the button is a toggle button, false if it is a simple one

## bool isToggleable () const

Returns the current value indicating if the button is a toggle button or a simple one. The default is 0.
### Return value

true if the button is a toggle button, false if it is a simple one
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the button. The default is 1.
### Arguments

- *int* **background** - The flag indicating whether a background texture is rendered for the button

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the button. The default is 1.
### Return value

Current flag indicating whether a background texture is rendered for the button
---

## static WidgetButtonPtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a button with a given label and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new button will belong.
- *const char ** **str** - Button label. This is an optional parameter.

## static WidgetButtonPtr create ( const char * str = 0 )

Constructor. Creates a button with a given label and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Button label. This is an optional parameter.

## void setImage ( const Ptr < Image > & image )

Sets a new image for the button.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cpp.md)* instead.

### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getImage ( ) const

Returns the current button image.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cpp.md)* instead.

### Return value

Button image.
## void setStyleImage ( const Ptr < Image > & image )

Sets a button skin image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to set.

## Ptr < Image > getStyleImage ( ) const

Returns the button skin image.
### Return value

Button skin image.
