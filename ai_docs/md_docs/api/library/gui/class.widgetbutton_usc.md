# Unigine::WidgetButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


Interface for widget button handling.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/button.png)


Here is an example of two buttons. Button1 has a background and image, Button2 is without them:


![](../../../code/gui/ui/examples/button.png)


> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture/image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.


#### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


### Example


The following code illustrates how to create a button widget and set its parameters.


## WidgetButton Class

### Members

## void setStyleTexture ( string texture )

Sets a new path to the button skin texture.
### Arguments

- *string* **texture** - The path to the button skin texture

## const char * getStyleTexture () const

Returns the current path to the button skin texture.
### Return value

Current path to the button skin texture
## void setText ( string text )

Sets a new button text label.
### Arguments

- *string* **text** - The button text label

## const char * getText () const

Returns the current button text label.
### Return value

Current button text label
## void setTextAlign ( int align )

Sets a new alignment of the button label. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_usc.md) variables.
### Arguments

- *int* **align** - The alignment of the button label

## int getTextAlign () const

Returns the current alignment of the button label. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_usc.md) variables.
### Return value

Current alignment of the button label
## void setTexture ( string texture )

Sets a new path to the button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Arguments

- *string* **texture** - The path to the button image texture

## const char * getTexture () const

Returns the current path to the button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Return value

Current path to the button image texture
## void setButtonColor ( vec4 color )

Sets a new color for the button.
### Arguments

- *vec4* **color** - The color for the button, as a four-component RGBA vector

## vec4 getButtonColor () const

Returns the current color for the button.
### Return value

Current color for the button, as a four-component RGBA vector
## void setToggled ( int toggled )

Sets a new value indicating if the toggle button is pressed.
### Arguments

- *int* **toggled** - The true if the toggle button is pressed, false if it is released

## int isToggled () const

Returns the current value indicating if the toggle button is pressed.
### Return value

Current true if the toggle button is pressed, false if it is released
## void setToggleable ( int toggleable )

Sets a new value indicating if the button is a toggle button or a simple one. The default is 0.
### Arguments

- *int* **toggleable** - The true if the button is a toggle button, false if it is a simple one

## int isToggleable () const

Returns the current value indicating if the button is a toggle button or a simple one. The default is 0.
### Return value

Current true if the button is a toggle button, false if it is a simple one
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the button. The default is 1.
### Arguments

- *int* **background** - The flag indicating whether a background texture is rendered for the button

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the button. The default is 1.
### Return value

Current flag indicating whether a background texture is rendered for the button
---

## static WidgetButton ( Gui gui , string str = 0 )

Constructor. Creates a button with a given label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new button will belong.
- *string* **str** - Button label. This is an optional parameter.

## static WidgetButton ( string str = 0 )

Constructor. Creates a button with a given label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Button label. This is an optional parameter.

## void setImage ( Image image )

Sets a new image for the button.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getImage ( )

Returns the current button image.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Return value

Button image.
## void setStyleImage ( Image image )

Sets a button skin image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getStyleImage ( )

Returns the button skin image.
### Return value

Button skin image.
