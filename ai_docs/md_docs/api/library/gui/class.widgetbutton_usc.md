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

## void setBackground ( int background )

Sets a value indicating if a background texture should be rendered for the button.
### Arguments

- *int* **background** - Positive number to render a background texture, **0** not to render.

## int getBackground ( )

Returns a value indicating if a background texture is rendered for the button.
### Return value

Positive number if a background texture is rendered; otherwise, **0**.
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
## void setText ( string text )

Sets a button text label.
### Arguments

- *string* **text** - Button label.

## string getText ( )

Returns the button text label.
### Return value

Button label.
## void setTextAlign ( int align )

Sets alignment of the button label.
### Arguments

- *int* **align** - One of the [*GUI_ALIGN_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.

## int getTextAlign ( )

Returns the alignment of the button label.
### Return value

One of the [*GUI_ALIGN_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.
## void setTexture ( string texture )

Sets a new texture to be used as the button image.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Arguments

- *string* **texture** - Path to a texture file.

## string getTexture ( )

Returns the path to the current button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_usc.md)* instead.

### Return value

Path to the button image.
## void setToggleable ( int toggleable )

Sets a value indicating if the button is a toggle button or a simple one.
### Arguments

- *int* **toggleable** - Positive number to make the button a toggle button, **0** to make it a simple one.

## int isToggleable ( )

Returns a value indicating if the button is a toggle button or a simple one.
### Return value

Positive number if the button is a toggle button; otherwise, **0**.
## void setToggled ( int toggled )

Sets a state of the toggle button.
### Arguments

- *int* **toggled** - Positive number to press the button, **0** to release it.

## int isToggled ( )

Returns a value indicating if the toggle button is pressed.
### Return value

**1** if the button is pressed; otherwise, **0**.
## void setButtonColor ( vec4 color )

Sets the color to be used for the button.
### Arguments

- *vec4* **color** - Four-component vector specifying the color in the RGBA format.

## vec4 getButtonColor ( )

Returns the current color for the button.
### Return value

Four-component vector specifying the color in the RGBA format.
## void setStyleImage ( Image image )

Sets a button skin image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to set.

## Image getStyleImage ( )

Returns the button skin image.
### Return value

Button skin image.
## void setStyleTexture ( string texture )

Sets a button skin texture.
### Arguments

- *string* **texture** - Path to a texture file.

## string getStyleTexture ( )

Returns the path to the button skin texture.
### Return value

Path to a texture file.
